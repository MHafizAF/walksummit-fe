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
    const sisa_kuota = responseJson.data.sisa_kuota;
    const jumlah_pendaki = responseJson.data.jumlah_pendaki;
    const kuota_maksimal = responseJson.data.kuota_maksimal;
    console.log(kuota_maksimal);
    const jumlahPendakiContent = document.querySelector(".jumlah-pendaki");
    const tersisaKuotaContent = document.querySelector(".tersisa-kuota");
    const maksimalKuotaContent = document.querySelector(".maksimal-kuota");
    jumlahPendakiContent.innerHTML = jumlah_pendaki;
    tersisaKuotaContent.innerHTML = sisa_kuota;
    maksimalKuotaContent.innerHTML = kuota_maksimal;
  };
  show();
}
onMounted(() => {
  getAllKuota();
});
</script>

<template>
  <main id="main" tabindex="0">
    <section id="hero">
      <div class="welcome">
        <h1 tabindex="0">Pemesanan Tiket Pendakian Gunung</h1>
      </div>
    </section>
    <section id="informasi-gunung">
      <h2 tabindex="0">Informasi Gunung</h2>
      <div class="informasi-detail-gunung">
        <p tabindex="0" aria-label="Ketinggian 3.153 mdpl">
          <i class="fa-solid fa-mountain"></i>3.153 mdpl
        </p>
        <p tabindex="0" aria-label="Berstatus Semi Aktif">
          <i class="fa-solid fa-volcano"></i>Semi Aktif
        </p>
        <p tabindex="0" aria-label="Harga Tiket Masuk 25 ribu">
          <i class="fa-solid fa-money-bill-wave"></i>Rp.25,000 (Tiap Jalur)
        </p>
        <p tabindex="0" aria-label="Kledung Jalur favorit">
          <i class="fa-solid fa-road"></i>Kledung (via favorite)
        </p>
        <p tabindex="0">
          <i class="fa-solid fa-compass"></i>7.3010463°S 109.9968767°E
        </p>
        <p tabindex="0">
          <i class="fa-solid fa-location-dot"></i>Desa Katekan, Kecamatan
          Ngadirejo
        </p>
        <p tabindex="0">
          <i class="fa-solid fa-map"></i>Kabupaten Temanggung, dan Kabupaten
          Wonosobo.
        </p>
        <iframe
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d31659.65199144163!2d109.97832366852224!3d-7.302499512684031!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x2e70757555351a43%3A0x6e1fd0eaed14acb5!2sGn.%20Sindoro!5e0!3m2!1sid!2sid!4v1654936415761!5m2!1sid!2sid"
          allowfullscreen=""
          loading="lazy"
          tittle="Location Sindoro Mountain"
          referrerpolicy="no-referrer-when-downgrade"
          tabindex="0"
        ></iframe>
      </div>
      <h2 tabindex="0">Informasi Pendaki Gunung</h2>
      <div class="informasi-pendaki-gunung">
        <div class="jumlah card">
          <h1><i class="fa-solid fa-user-check"></i></h1>
          <h3 tabindex="0">Jumlah Saat Ini</h3>
          <p class="jumlah-pendaki" tabindex="0">30</p>
        </div>
        <div class="tersisa card">
          <h1><i class="fa-solid fa-users"></i></h1>
          <h3 tabindex="0">Kuota Tersisa</h3>
          <p class="tersisa-kuota" tabindex="0">30</p>
        </div>
        <div class="maksimal card">
          <h1><i class="fa-solid fa-users-between-lines"></i></h1>
          <h3 tabindex="0">Maksimal Perhari</h3>
          <p class="maksimal-kuota" tabindex="0">30</p>
        </div>
      </div>
    </section>
    <section id="alur-daftar-pendaki">
      <h2 tabindex="0">Alur Pendaftaran Pendakian</h2>

      <div class="alur-daftar-container">
        <div class="alur-daftar-1">
          <h1 tabindex="0" aria-label="pertama">1</h1>
          <picture>
            <source />
            <img src="../../public/images/alur/alur-1.jpg" alt="Alur Pertama" />
          </picture>
          <p tabindex="0">Pendaki harap membaca halaman home terlebih dahulu</p>
        </div>

        <div class="alur-daftar-2">
          <h1 tabindex="0" aria-label="kedua">2</h1>
          <picture>
            <source />
            <img src="../../public/images/alur/alur-2.png" alt="Alur Kedua" />
          </picture>
          <p tabindex="0">
            Cek Kuota Jalur yang tersedia sebelum mendaftar pendakian
          </p>
        </div>

        <div class="alur-daftar-3">
          <h1 tabindex="0" aria-label="ketiga">3</h1>
          <picture>
            <source />
            <img src="../../public/images/alur/alur-3.png" alt="Alur Ketiga" />
          </picture>
          <p tabindex="0">Para pendaki harap baca dan pahami SOP Pendakian</p>
        </div>

        <div class="alur-daftar-4">
          <h1 tabindex="0" aria-label="keempat">4</h1>
          <picture>
            <source />
            <img src="../../public/images/alur/alur-4.png" alt="Alur Keempat" />
          </picture>
          <p tabindex="0">Pilih Navigasi Daftar, masukan tanggal & jalur</p>
        </div>

        <div class="alur-daftar-5">
          <h1 tabindex="0" aria-label="kelima">5</h1>
          <picture>
            <source />
            <img src="../../public/images/alur/alur-5.png" alt="Alur Kelima" />
          </picture>
          <p tabindex="0">
            Setelah itu klik tombol tambah pendaki untuk mengisi biodata
          </p>
        </div>

        <div class="alur-daftar-6">
          <h1 tabindex="0" aria-label="keenam">6</h1>
          <picture>
            <source />
            <img src="../../public/images/alur/alur-6.png" alt="Alur Keenam" />
          </picture>
          <p tabindex="0">Jika sudah harap menunggu untuk diberikan ID Grub</p>
        </div>

        <div class="alur-daftar-7">
          <h1 tabindex="0" aria-label="ketujuh">7</h1>
          <picture>
            <source />
            <img src="../../public/images/alur/alur-7.png" alt="Alur Ketujuh" />
          </picture>
          <p tabindex="0">
            Setelah itu hubungi kontak yang tersedia untuk verifikasi
          </p>
        </div>

        <div class="alur-daftar-8">
          <h1 tabindex="0" aria-label="kedelapan">8</h1>
          <picture>
            <source />
            <img
              src="../../public/images/alur/alur-8.png"
              alt="Alur Kedelapan"
            />
          </picture>
          <p tabindex="0">
            Jika sudah status akan berubah "LUNAS" di halaman pencarian
          </p>
        </div>
      </div>
      <div class="container">
        <a class="daftar" href="/daftar">Ingin daftar mendaki ?</a>
      </div>
    </section>
    <section id="galeri-gunung">
      <h2 tabindex="0">Galeri Gunung</h2>
      <div class="list-galeri">
        <picture>
          <source />
          <img srcset="../../public/images/ke-1.jpg" alt="gunung preview" />
        </picture>
        <picture>
          <source />
          <img srcset="../../public/images/ke-2.jpg" alt="gunung preview" />
        </picture>
        <picture>
          <source />
          <img
            srcset="../../public/images/gunungsindoro.jpg"
            alt="gunung preview"
          />
        </picture>
      </div>
    </section>
    <section id="contact">
      <h2 tabindex="0" aria-label="Hubungi Kami">Contact Us</h2>
      <hr />
      <div class="list">
        <div class="box">
          <h1><i class="fa-solid fa-face-grin-wink"></i></h1>
          <p tabindex="0" aria-label="083434342">(+62) 83434342</p>
        </div>
        <div class="box">
          <h1><i class="fa-solid fa-face-grin-wink"></i></h1>
          <p tabindex="0" aria-label="083434342">(+62) 83434342</p>
        </div>
        <div class="box">
          <h1><i class="fa-solid fa-face-grin-wink"></i></h1>
          <p tabindex="0" aria-label="083434342">(+62) 83434342</p>
        </div>
        <div class="box">
          <h1><i class="fa-solid fa-face-grin-wink"></i></h1>
          <p tabindex="0" aria-label="083434342">(+62) 83434342</p>
        </div>
      </div>
    </section>
  </main>
</template>

<style scoped lang="scss">
main {
  width: 100%;
  height: 100vh;
  margin-top: 80px;
  .skip-link {
    position: absolute;
    top: -40px;
    left: 0;
    background-color: #f8b400;
    color: black;
    padding: 8px;
    z-index: 100;
  }
  .skip-link:focus {
    top: 0;
  }
  #hero {
    position: relative;
    z-index: -2;
    margin-bottom: 40px;
    picture {
      img {
        width: 100%;
        object-fit: cover;
        object-position: center;
      }
    }
    .welcome {
      width: 100%;
      height: 450px;
      padding: 10px 20px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      background-image: url("../../public/images/sindoro.jpg");
      background-size: cover;
      background-position: center;
      background-repeat: no-repeat;
      h1 {
        font-family: "Lobster", cursive;
        font-size: 50px;
        text-align: center;
        color: white;
      }
    }
  }
  #informasi-gunung {
    width: 100%;
    display: flex;
    padding: 10px 20px;
    margin: 0 auto;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 15px;
    h2 {
      font-family: "Quicksand";
      font-size: 30px;
      margin: 30px 0;
    }
    .informasi-detail-gunung {
      width: 80%;
      padding: 30px 40px;
      margin-bottom: 40px;
      display: flex;
      flex-direction: column;
      gap: 5px;
      font-size: 18px;
      background-color: #dbdffd;
      box-shadow: rgba(100, 100, 111, 0.2) 0px 5px 15px 0px;
      border-radius: 10px;
      .fa-solid {
        width: 20px;
        height: 20px;
        margin-right: 15px;
      }
      p {
        font-family: "Quicksand";
        font-weight: 800;
        font-size: 20px;
        margin-bottom: 10px;
      }
      iframe {
        width: 100%;
        height: 450px;
        margin: 20px 0;
        border-radius: 10px;
      }
    }
    .informasi-pendaki-gunung {
      width: 60%;
      padding: 20px 40px;
      margin-bottom: 40px;
      display: flex;
      justify-content: center;
      font-size: 18px;
      background-color: #dbdffd;
      box-shadow: rgba(100, 100, 111, 0.2) 0px 5px 15px 0px;
      border-radius: 10px;
      .card {
        margin: 20px 50px;
        text-align: center;
        h1 {
          font-size: 50px;
          margin-bottom: 10px;
        }
        h3 {
          font-family: "Quicksand";
          font-weight: 800;
          margin-bottom: 10px;
        }
        p {
          font-family: "Quicksand";
          font-weight: 800;
          font-size: 50px;
        }
      }
    }
  }
  #alur-daftar-pendaki {
    width: 80%;
    display: flex;
    flex-direction: column;
    gap: 20px;
    justify-content: center;
    align-items: center;
    padding: 10px 20px;
    margin: 0 auto 40px auto;
    h2 {
      font-family: "Quicksand";
      font-weight: 800;
      font-size: 30px;
      margin: 30px 0;
    }
    picture {
      margin: 10px 0;
    }
    p {
      text-align: center;
    }
    .alur-daftar-container {
      display: grid;
      gap: 20px;
      grid-template-columns: repeat(1, 1fr);
      font-family: "Quicksand";
      font-weight: 800;
      .alur-daftar-1,
      .alur-daftar-2,
      .alur-daftar-3,
      .alur-daftar-4,
      .alur-daftar-5,
      .alur-daftar-6,
      .alur-daftar-7,
      .alur-daftar-8,
      .alur-daftar-9 {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        padding: 20px 20px;
        gap: 10px;
        border-radius: 10px;
        picture {
          img {
            width: 100%;
            aspect-ratio: 1/1;
            min-height: 400px;
            max-height: 800px;
            background-color: #ffffff;
            padding: 10px;
            border-radius: 5px;
            box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
          }
        }
      }
    }
    .container {
      display: flex;
      padding: 20px 20px;
      margin-top: 20px;
      border-radius: 10px;
      flex-direction: column;
      align-items: center;
      background-color: #dbdffd;
    }
    .daftar {
      font-family: "Quicksand";
      font-weight: 800;
      color: black;
      position: relative;
      z-index: 0;
    }
    .daftar::after {
      position: absolute;
      content: "";
      width: 0%;
      height: 4px;
      background-color: green;
      left: 50%;
      bottom: -10px;
      transition: all 0.4s ease-in-out;
    }
    .container:hover {
      cursor: pointer;
    }
    .container:hover .daftar::after {
      width: 100%;
      left: 0;
    }
  }
  #galeri-gunung {
    width: 90%;
    margin: 0 auto;
    display: flex;
    padding: 10px 20px;
    margin-bottom: 40px;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 10px;
    h2 {
      font-family: "Quicksand";
      font-size: 30px;
      margin: 30px 0;
    }
    .list-galeri {
      display: grid;
      grid-template-columns: repeat(1, 1fr);
      justify-content: center;
      align-items: center;
      gap: 10px;
      picture {
        background-color: rgb(236, 237, 254);
        padding: 20px;
        img {
          width: 100%;
          height: 300px;
          background-color: #9d9a9a;
        }
      }
    }
  }
  #contact {
    width: 80%;
    padding: 20px;
    margin: 0 auto 40px auto;
    h2 {
      font-family: "Quicksand";
      margin: 30px 0;
    }
    .list {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      padding: 16px;
      .box {
        margin: 0 40px;
        text-align: center;
        h1 {
          font-size: 50px;
          margin-bottom: 13px;
        }
        p {
          font-family: "Quicksand";
          font-weight: 800;
          font-size: 20px;
          margin-bottom: 10px;
        }
      }
    }
  }
}
@media only screen and (max-width: 600px) {
  main {
    #hero {
      .welcome {
        height: 200px;
        h1 {
          font-size: 25px;
        }
      }
    }
    #informasi-gunung {
      h2 {
        font-size: 20px;
      }
      .informasi-detail-gunung {
        padding: 16px;
        width: 90%;
        .fa-solid {
          width: 10px;
          height: 10px;
        }
        p {
          font-size: 15px;
        }
        iframe {
          width: 100%;
          height: 250px;
        }
      }
      .informasi-pendaki-gunung {
        width: 90%;
        display: flex;
        flex-wrap: wrap;
      }
    }
    #alur-daftar-pendaki {
      h2 {
        font-size: 20px;
        margin: 10px 0;
      }
    }
    #contact {
      width: 100%;
      h2 {
        font-size: 20px;
      }
      .list {
        grid-template-columns: repeat(2, 1fr);
        gap: 10px;
        .box {
          h1 {
            font-size: 40px;
          }
          p {
            font-size: 15px;
          }
        }
      }
    }
  }
}

@media only screen and (min-width: 601px) {
  main {
    #hero {
      .welcome {
        height: 300px;
        h1 {
          font-size: 35px;
        }
      }
    }
    #informasi-gunung {
      .informasi-detail-gunung {
        width: 90%;
        iframe {
          width: 100%;
          height: 250px;
        }
      }
      .informasi-pendaki-gunung {
        width: 80%;
        display: flex;
        flex-wrap: wrap;
      }
    }
    #contact {
      width: 90%;
      h2 {
        font-size: 30px;
      }
      .list {
        grid-template-columns: repeat(2, 1fr);
        gap: 10px;
        .box {
          h1 {
            font-size: 40px;
          }
          p {
            font-size: 15px;
          }
        }
      }
    }
  }
}

@media only screen and (min-width: 768px) {
  main {
    #hero {
      .welcome {
        height: 350px;
        h1 {
          font-size: 35px;
        }
      }
    }
    #informasi-gunung {
      .informasi-detail-gunung {
        padding: 26px;
        width: 90%;
        .fa-solid {
          width: 20px;
          height: 20px;
        }
        p {
          font-size: 20px;
        }
        iframe {
          width: 100%;
          height: 250px;
        }
      }
      .informasi-pendaki-gunung {
        width: 80%;
        display: flex;
        flex-wrap: wrap;
      }
    }

    #alur-daftar-pendaki {
      .alur-daftar-container {
        grid-template-columns: repeat(2, 1fr);
      }
    }
    #galeri-gunung {
      .list-galeri {
        grid-template-columns: repeat(1, 1fr);
      }
    }
    #contact {
      width: 90%;
      h2 {
        font-size: 30px;
      }
      .list {
        grid-template-columns: repeat(4, 1fr);
        gap: 10px;
        .box {
          h1 {
            font-size: 40px;
          }
          p {
            font-size: 15px;
          }
        }
      }
    }
  }
}

@media only screen and (min-width: 1020px) {
  main {
    margin-top: 70px;
    #hero {
      .welcome {
        height: 300px;
        h1 {
          font-size: 30px;
        }
      }
    }
    #informasi-gunung {
      h2 {
        font-size: 25px;
      }
      .informasi-detail-gunung {
        width: 100%;
        p {
          font-size: 16px;
        }
        iframe {
          width: 100%;
          height: 350px;
        }
      }
      .informasi-pendaki-gunung {
        width: 60%;
        display: flex;
        flex-wrap: nowrap;
        .card {
          h1 {
            font-size: 40px;
          }
          h3 {
            font-size: 16px;
          }
        }
      }
    }
    #alur-daftar-pendaki {
      width: 100%;
      h2 {
        font-size: 25px;
      }
      .alur-daftar-container {
        grid-template-columns: repeat(3, 1fr);
      }
    }
    #galeri-gunung {
      width: 80%;
      h2 {
        font-size: 25px;
      }
      .list-galeri {
        grid-template-columns: repeat(2, 1fr);
      }
    }
  }
}
@media only screen and (min-width: 1200px) {
  main {
    margin-top: 70px;
    #hero {
      .welcome {
        height: 450px;
        h1 {
          font-size: 50px;
        }
      }
    }
    #informasi-gunung {
      h2 {
        font-size: 30px;
      }
      .informasi-detail-gunung {
        width: 80%;
        p {
          font-size: 20px;
        }
        iframe {
          width: 100%;
          height: 450px;
        }
      }
      .informasi-pendaki-gunung {
        width: 50%;
        display: flex;
        flex-wrap: nowrap;
      }
    }
    #alur-daftar-pendaki {
      width: 80%;
      h2 {
        font-size: 30px;
      }
      .alur-daftar-container {
        grid-template-columns: repeat(3, 1fr);
        img {
          width: 100%;
          height: 200px;
        }
      }
    }
    #galeri-gunung {
      width: 80%;
      h2 {
        font-size: 30px;
      }
      .list-galeri {
        grid-template-columns: repeat(3, 1fr);
      }
    }
    #contact {
      width: 80%;
      h2 {
        font-size: 30px;
      }
      hr {
        height: 6px;
        background-color: #354259;
      }
      .list {
        margin-top: 20px;
        .box {
          h1 {
            font-size: 50px;
          }
          p {
            font-size: 20px;
          }
        }
      }
    }
  }
}
@media only screen and (min-width: 1600px) {
  main {
    margin-top: 70px;
    #hero {
      .welcome {
        height: 650px;
        h1 {
          font-size: 80px;
        }
      }
    }
    #informasi-gunung {
      h2 {
        font-size: 50px;
      }
      .informasi-detail-gunung {
        width: 80%;
        .fa-solid {
          width: 30px;
          height: 30px;
        }
        p {
          font-size: 30px;
        }
        iframe {
          width: 100%;
          height: 600px;
        }
      }
      .informasi-pendaki-gunung {
        width: 50%;
        .card {
          margin: 20px 50px;
          text-align: center;
          h1 {
            font-size: 80px;
            margin-bottom: 10px;
          }
          h3 {
            font-family: "Quicksand";
            font-weight: 800;
            font-size: 40px;
            margin-bottom: 10px;
          }
          p {
            font-family: "Quicksand";
            font-weight: 800;
            font-size: 80px;
          }
        }
      }
    }
    #alur-daftar-pendaki {
      width: 80%;
      h2 {
        font-size: 50px;
      }
      h1 {
        font-size: 30px;
      }
      p {
        font-size: 30px;
      }
      .alur-daftar-container {
        grid-template-columns: repeat(4, 1fr);
        img {
          width: 100%;
          height: 500px;
        }
      }
      .container {
        width: 350px;
        padding: 20px;
        font-size: 30px;
      }
    }
    #galeri-gunung {
      width: 80%;
      h2 {
        font-size: 50px;
      }
    }
    #contact {
      width: 80%;
      h2 {
        font-size: 50px;
      }
      hr {
        height: 6px;
        background-color: #354259;
      }
      .list {
        margin-top: 20px;
        .box {
          h1 {
            font-size: 70px;
          }
          p {
            font-size: 30px;
          }
        }
      }
    }
  }
}
</style>
