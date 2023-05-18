<script setup>
import axios from "axios";
import { ref, onMounted } from "vue";
import CardKuota from "../components/CardKuota.vue";

const dataKuota = ref([]);

// method for get data kuota
async function getAllKuota() {
  await axios
    .get(`${import.meta.env.VITE_API}/api/informasi-gunung`)
    .then(function (response) {
      dataKuota.value = response.data.data.kuota_tiap_jalur;
    })
    .catch((error) => console.log(error));
}

// run method gerallkuoata when page mounted
onMounted(() => {
  getAllKuota();
});
</script>

<template>
  <main id="main" tabindex="0">
    <div class="header">
      <h1>Kuota Tiap Jalur</h1>
    </div>
    <CardKuota v-for="(value, index) in dataKuota" :key="index" :item="value" />
  </main>
</template>

<style scoped lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Lobster&family=Ms+Madi&family=Quicksand:wght@300&family=Rock+Salt&display=swap");
main {
  margin-top: 84px;
  padding: 20px;
  min-height: 100vh;
  h1 {
    text-align: center;
    font-family: "Quicksand", sans-serif;
  }
  .content {
    width: 70%;
    margin: 40px auto;
  }
}
@media only screen and (max-width: 600px) {
  main {
    .header {
      hr {
        width: 80%;
      }
    }
    .content {
      width: 100%;
      h2 {
        font-size: 20px;
      }
      h3 {
        font-size: 16px;
      }
    }
  }
}
@media only screen and (min-width: 1024px) {
  main {
    h1 {
      font-size: 25px;
    }
  }
}
@media only screen and (min-width: 1200px) {
  main {
    h1 {
      font-size: 30px;
    }
  }
}
</style>
