<script setup>
import { reactive } from "@vue/reactivity";
import axios from "axios";
//import { stat } from "fs";
function search(searchID) {
  // const list = listForm;
  // const listJson = JSON.stringify(list);
  // const listJsonParse = JSON.parse(listJson);
  // console.log(listJsonParse);
  // const filterID = listJsonParse.filter((grup) =>
  //   grup.id == searchID ? grup : null
  // );
  // console.log(filterID);
  const searchGrup = async () => {
    const { data } = await axios
      .get(`${import.meta.env.VITE_API}/api/cari-grup/${searchID}`)
      .then(function (response) {
        return response;
      })
      .catch(() => {
        const listContainer = document.querySelector("#list-grup");
        listContainer.innerHTML = `<p tabindex="0">Data Tidak Ditemukan</p>`;
      });
    return data;
  };

  const show = async () => {
    const responseJson = await searchGrup();
    console.log(responseJson.data);
    const id = responseJson.data.id;
    const nama = responseJson.data.koordinator;
    const statusPembayaran =
      responseJson.data.status == 0 ? "Belum Bayar" : "Sudah Lunas";
    const jalur = responseJson.data.jalur;
    const listContainer = document.querySelector("#list-grup");

    listContainer.innerHTML = `
        <div id="info-grup">
          <p tabindex="0">Id Grup: ${id}</p>
          <p tabindex="0">Nama Koordinator: ${nama}</p>
          <p class="status-text" tabindex="0">Status Pembayaran: <span class="status-bayar">${statusPembayaran}</span></p>
          <p tabindex="0">Jalur: ${jalur}</p>
        </div>
        <style>
        #info-grup{
          background-color: rgb(146, 198, 254);
          padding: 10px;
          border-radius: 5px;
        }
        #info-grup p {
          margin: 10px 10px;
          font-family: 'Quicksand', sans-serif;
          text-transform: uppercase;
        }</style>`;
    listContainer.style.display = "flex";
    listContainer.style.flexDirection = "column";
    listContainer.style.gap = "20px";
    if (statusPembayaran == "Belum Bayar") {
      const status = document.querySelector(".status-bayar");
      status.style.backgroundColor = "red";
      status.style.padding = "10px";
      status.style.borderRadius = "10px";
      status.style.fontWeight = "bolder";
    } else {
      const status = document.querySelector(".status-bayar");
      status.style.backgroundColor = "green";
      status.style.padding = "10px";
      status.style.borderRadius = "10px";
      status.style.fontWeight = "bolder";
    }
    const statusText = document.querySelector(".status-text");
    statusText.style.display = "flex";
    statusText.style.alignItems = "center";
    statusText.style.gap = "10px";
    const small = window.matchMedia("(max-width: 600px)");
    function resizeImage(size) {
      if (size.matches) {
        statusText.style.flexDirection = "row";
      }
    }
    resizeImage(small);
  };
  show();
}

function clearSearch() {
  const listContainer = document.querySelector("#list-grup");
  const inputSearch = document.querySelector("#idsearch");
  inputSearch.value = "";
  listContainer.innerHTML = "";
}
</script>

<template>
  <main id="main" tabindex="0">
    <h1>Grub Pendaki</h1>
    <form @submit.prevent="search(searchID)">
      <label for="idsearch" tabindex="0" aria-label="Pencarian Grub"
        >Cari Id Grup:</label
      >
      <input
        type="search"
        id="idsearch"
        name="idsearch"
        placeholder="Search.."
        v-model="searchID"
        aria-label="kolom pencarian"
        @input="searchInput(searchID)"
      />
    </form>
    <div class="search-button-container">
      <button type="submit" class="btn btn-white" aria-label="Mulai Mencari">
        Search
      </button>
      <button
        type="submit"
        class="btn btn-red"
        @click="clearSearch()"
        aria-label="Menghapus Pencarian"
      >
        Clear
      </button>
    </div>

    <div id="hasil-search-container">
      <h2 tabindex="0">Hasil Pencarian</h2>
      <div id="list-grup"></div>
    </div>
  </main>
</template>

<style scoped lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Lobster&family=Ms+Madi&family=Quicksand:wght@300&family=Rock+Salt&display=swap");

main {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  padding: 10px 20px;
  margin-top: 80px;
  gap: 10px;
  h1 {
    font-family: "Quicksand", sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 20px;
  }
  form {
    width: 70%;
    margin: 20px auto;
    display: flex;
    flex-direction: column;
    gap: 10px;
    label {
      font-family: "Quicksand", sans-serif;
      font-size: 22px;
      font-weight: bold;
    }
    input {
      padding: 10px;
      border-radius: 10px;
      height: 50px;
      font-family: "Quicksand", sans-serif;
      font-size: 20px;
      color: black;
    }
  }
  .search-button-container {
    display: flex;
    justify-content: center;
    gap: 5px;
    button {
      padding: 5px 20px;
      border-radius: 10px;
      font-weight: bold;
      font-family: "Quicksand", sans-serif;
    }

    .btn:hover {
      transform: translateY(-3px);
      box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
      cursor: pointer;
    }

    .btn:active {
      transform: translateY(-1px);
      box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
    }

    .btn-white {
      background-color: rgb(143, 188, 144);
      color: black;
      font-size: 16px;
    }
    .btn-red {
      background-color: rgb(255, 110, 66);
      color: black;
      font-size: 16px;
    }
  }
  #hasil-search-container {
    display: flex;
    width: 60%;
    margin: 30px auto;
    flex-direction: column;
    gap: 20px;
    h2 {
      font-family: "Quicksand", sans-serif;
      text-align: center;
    }
    #list-grup {
      padding: 10px;
      border-radius: 10px;
      background-color: #dbdffd;
      box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px,
        rgba(0, 0, 0, 0.3) 0px 8px 16px -8px;
      font-size: medium;
      font-weight: bold;
    }
  }
}
@media only screen and (max-width: 600px) {
  main {
    width: 100%;
    form {
      width: 100%;
    }
    #hasil-search-container {
      width: 90%;
    }
  }
}
@media only screen and (min-width: 1020px) {
  main {
    margin-top: 70px;
    h1 {
      font-size: 25px;
    }
  }
}
@media only screen and (min-width: 1200px) {
  main {
    margin-top: 70px;
    h1 {
      font-size: 30px;
    }
  }
}
</style>
