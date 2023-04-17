<script setup>
import FormBiodata from "../components/FormBiodata.vue";
import { reactive, ref } from "@vue/reactivity";
import ModalAlert from "../components/ModalAlert.vue";
import { onMounted } from "vue";
const emit = defineEmits(["formChanges"]);
import axios from "axios";

const forms = reactive([]);

const formsPendakian = reactive({
  berangkat: "",
  pulang: "",
  jalur: "",
});

function callback(id, form) {
  const targetIndex = forms.findIndex((form) => form.id == id);
  forms[targetIndex] = form;
}
function addForm() {
  forms.push({
    id: Date.now(),
    nik: "",
    nama: "",
    gender: "",
    alamat: "",
    noHp: "",
    noHpOrtu: "",
  });
}
function checkForms() {
  let jalur = document.querySelector(".jalur").value;
  let berangkat = document.querySelector(".input-berangkat").value;
  let pulang = document.querySelector(".input-pulang").value;

  const tambahGrup = async () => {
    let alertRequired = document.querySelector(".alert-required");
    if (!jalur || !berangkat || !pulang) {
      alertRequired.innerHTML = `
      <div class="message-alert">
      <p>* Semua Input Wajib diisi</p>
      </div>
      <style>
      .message-alert{
        display: flex;
        padding: 0px 20px 20px 20px;
      }
      .message-alert p {
        display: flex;
        color: red;
        padding: 10px;
        font-family: 'Quicksand';
        font-weight: bold;
        font-style: italic;
        background-color: white;
        border-radius: 10px;
      }
      </style>
      `;
    } else {
      const data = await axios
        .post(`${import.meta.env.VITE_API}/api/tambah-grup`, {
          jalur_id: jalur,
          tgl_brangkat: berangkat,
          tgl_pulang: pulang,
        })
        .then(function (response) {
          return response.data.data.id;
        })
        .catch((error) => console.log(error));
      return data;
    }
  };

  const anggota = forms.map((form) => ({
    nik: form.nik,
    alamat: form.alamat,
    nama: form.nama,
    no_telp: form.noHp,
    no_telp_orgtua: form.noHpOrtu,
    jenis_kelamin: form.gender,
  }));

  const stringJSON = JSON.stringify(anggota);
  const objectBiasa = JSON.parse(stringJSON);

  const tambahPendaki = async () => {
    const idGrup = await tambahGrup();
    idGroupPendakian.value = idGrup;
    let inputForm = document.querySelectorAll("input");
    let alertTambah = document.querySelector(".alert-tambah-pendaki");
    objectBiasa.forEach(async (object) => {
      if (!inputForm.value) {
        let tesValue = inputForm.forEach((form) => {
          let valueForm = form.value;
          if (!valueForm) {
            alertTambah.innerHTML = `
          <div class="message-alert-tambah">
            <p>Semua Input Wajib diisi</p>
          </div>
          <style>
          .message-alert-tambah{
            display: flex;
            padding: 20px 20px 0px 20px;
          }
          .message-alert-tambah p {
            display: flex;
            color: white;
            padding: 10px;
            font-weight: bold;
            background-color: red;
            border-radius: 10px;
          }
          </style>
          `;
          }
        });
      }
      const data = await axios
        .post(`${import.meta.env.VITE_API}/api/tambah-pelanggan`, {
          grup_id: idGrup,
          nik: object.nik,
          nama: object.nama,
          alamat: object.alamat,
          no_telp: object.no_telp,
          no_telp_orgtua: object.no_telp_orgtua,
          jenis_kelamin: object.jenis_kelamin,
        })
        .then(function () {
          handleOpenModal();
        })
        .catch((error) => console.log(error));
      return data;
    });
  };
  tambahPendaki();
}

const showModal = ref(false);

const handleOpenModal = () => {
  showModal.value = true;
};

const handleCloseModal = () => {
  showModal.value = false;
};

const jalurPendakian = ref({});

onMounted(() => {
  axios
    .get(`${import.meta.env.VITE_API}/api/jalur`)
    .then((response) => (jalurPendakian.value = response.data.data))
    .catch((err) => console.log(err));
});

const idGroupPendakian = ref("");
</script>

<template>
  <main id="main" tabindex="0">
    <h2 tabindex="0">Daftar Pendakian Gunung</h2>

    <div class="tanggal-container">
      <form action="">
        <label for="" tabindex="0">Tanggal Berangkat</label>
        <input
          class="input-berangkat"
          type="date"
          v-model="formsPendakian.berangkat"
          required
        />
        {{ berangkat }}
        <label for="" tabindex="0">Tanggal Pulang</label>
        <input
          class="input-pulang"
          type="date"
          v-model="formsPendakian.pulang"
          required
        />
        {{ pulang }}
        <label for="" tabindex="0">Pilih Jalur</label>
        <div class="select">
          <select
            class="jalur"
            name="jalur"
            id="jalur"
            v-model="formsPendakian.jalur"
            required
          >
            <option
              v-for="(value, index) in jalurPendakian"
              :key="index"
              :value="value.id"
            >
              {{ value.nama }}
            </option>
          </select>
        </div>
        {{ jalur }}
      </form>
      <div class="alert-required"></div>
    </div>
    <h2 tabindex="0">Informasi Pendaki</h2>
    <button
      class="add-button"
      @click="addForm"
      tabindex="0"
      aria-label="Masukan biodata pendaki"
    >
      <i class="fa-solid fa-user-plus"></i>Pendaki
    </button>
    <div class="alert-tambah-pendaki"></div>
    <div class="biodata-container">
      <form-biodata
        @formChanges="(n) => callback(form.id, n)"
        :foo.sync="form"
        v-for="form in forms"
      ></form-biodata>
    </div>
    <button
      @click.prevent="checkForms()"
      type="submit"
      tabindex="0"
      aria-label="Selesai Mendaftar"
    >
      <i class="fa-solid fa-circle-check"></i>Selesai
    </button>
    <!-- <div class="modal-container"></div> -->
    <ModalAlert
      v-if="showModal"
      @close="handleCloseModal"
      :idGrup="idGroupPendakian"
    />
  </main>
</template>

<style scoped lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Lobster&family=Ms+Madi&family=Quicksand:wght@300&family=Rock+Salt&display=swap");

main {
  width: 80%;
  display: flex;
  flex-direction: column;
  padding: 10px 20px;
  margin: 80px auto 0 auto;
  gap: 10px;
  min-height: 100vh;
  h2 {
    font-family: "Quicksand", sans-serif;
    margin: 25px 0 15px;
  }
  .tanggal-container {
    background-color: #dbdffd;
    border-radius: 20px;
    form {
      display: flex;
      gap: 10px;
      flex-direction: column;
      padding: 30px 20px;
      label {
        font-family: "Quicksand", sans-serif;
        font-weight: 800;
        font-size: 20px;
        margin: 10px 0;
        color: black;
      }
      input {
        font-family: "Quicksand", sans-serif;
        font-weight: 800;
        font-size: 18px;
        padding: 10px;
        border-radius: 8px;
      }
      select {
        -webkit-appearance: none;
        -moz-appearance: none;
        -ms-appearance: none;
        appearance: none;
        outline: 0;
        box-shadow: none;
        border: 0 !important;
        background: white;
        background-image: none;
        flex: 1;
        padding: 0 0.5em;
        color: black;
        cursor: pointer;
        font-size: 1em;
        font-family: "Quicksand", sans-serif;
        font-weight: 800;
      }
      select::-ms-expand {
        display: none;
      }
      .select {
        position: relative;
        display: flex;
        height: 2.5em;
        line-height: 2.5em;
        background: #5c6664;
        overflow: hidden;
        border-radius: 0.25em;
        border-radius: 8px;
      }
      .select::after {
        content: "\25BC";
        position: absolute;
        top: 0;
        right: 0;
        padding: 0 1em;
        background-color: #ca82ff;
        cursor: pointer;
        pointer-events: none;
        transition: 0.25s all ease;
      }
      .select:hover::after {
        color: #fbcb0a;
      }
    }
  }
  .biodata-container {
    display: grid;
    grid-template-columns: repeat(1, 1fr);
    gap: 15px;
    margin: 15px 0 30px 0;
    border-radius: 20px;
    form {
      display: flex;
      gap: 10px;
      flex-direction: column;
      padding: 20px 20px;
      input {
        padding: 5px;
        border-radius: 10px;
      }
      .radio-button {
        display: flex;
        gap: 10px;
      }
    }
  }
  .fa-solid {
    margin-right: 6px;
  }
  .add-button {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 10px 20px;
    width: 130px;
    height: 44px;
    font-weight: 800;
    background-color: white;
  }
  .add-button:hover {
    transform: translateY(-3px);
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
    cursor: pointer;
    opacity: 1;
    background-color: #f7d716;
  }
  button {
    background-color: white;
    color: #050b38;
    padding: 10px;
    margin-bottom: 10px;
    border-radius: 10px;
    font-family: "Quicksand", sans-serif;
    font-size: 20px;
    font-weight: 800;
    opacity: 0.8;
  }
  button:hover {
    transform: translateY(-3px);
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
    cursor: pointer;
    opacity: 1;
    background-color: #83bd75;
  }

  button:active {
    transform: translateY(-1px);
    box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
  }
}
@media only screen and (max-width: 600px) {
  main {
    width: 100%;
    .tanggal-container {
      form {
        .select {
          width: 60%;
        }
      }
    }
  }
}
@media only screen and (min-width: 768px) {
  main {
    width: 100%;
    .biodata-container {
      grid-template-columns: repeat(1, 1fr);
    }
    .tanggal-container {
      form {
        .select {
          width: 40%;
        }
      }
    }
  }
}
@media only screen and (min-width: 1020px) {
  main {
    width: 80%;
    margin-top: 70px;
    .biodata-container {
      grid-template-columns: repeat(2, 1fr);
    }
    .tanggal-container {
      form {
        .select {
          width: 40%;
        }
      }
    }
  }
}
@media only screen and (min-width: 1200px) {
  main {
    .biodata-container {
      grid-template-columns: repeat(3, 1fr);
    }
  }
}
</style>
