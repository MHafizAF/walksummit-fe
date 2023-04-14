<script setup>
import axios from "axios";
import { ref, onMounted } from "vue";
function getAllKuota() {
  const showKuota = async () => {
    const { data } = await axios
      .get(`${import.meta.env.VITE_API}/api/informasi-gunung`)
      .then(function (response) {
        return response;
      })
      .catch((error) => console.log(error));
    return data;
  };
  const show = async () => {
    const responseJson = await showKuota();
    console.log(responseJson.data);
    const jalur = responseJson.data.kuota_tiap_jalur;
    const jalurMap = jalur.map((jalur) => {
      const content = document.querySelector(".content");
      content.innerHTML += `
      <div class="card-jalur">
        <h2 tabindex="0">Via ${jalur.nama}</h2>
        <h3 tabindex="0">Sisa Kuota Hari ini : <i class="fa-solid fa-person-hiking"></i>${jalur.kuota}</h3>
      </div>
      <style>
      .content{
        display: flex;
        flex-direction: column;
        gap: 20px;
      }
      .card-jalur{
        display: flex;
        flex-direction: column;
        gap: 20px;
        padding: 16px;
        box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
        border-radius: 8px;
      }
      .fa-solid {
        margin-right: 6px;
        margin-left: 6px;
      }
      h2,h3{
          font-family: "Quicksand", sans-serif;
        }
      </style>
      `;
    });
  };
  show();
}
onMounted(() => {
  getAllKuota();
});
</script>

<template>
  <main id="main" tabindex="0">
    <div class="header">
      <h1>Kuota Tiap Jalur</h1>
    </div>
    <div class="content"></div>
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
