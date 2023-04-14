<template>
  <div class="modal-container">
    <div class="message-modal">
      <h1>
        <i class="fa-solid fa-triangle-exclamation"></i>Peringatan Walkers
      </h1>
      <h2>SIMPAN ID GRUP ANDA UNTUK</h2>
      <h3>"VERIFIKASI PEMBAYARAN"</h3>
      <p class="id-grup-modal">ID GRUP ANDA</p>
      <p class="id-grup">{{ idGrup }}</p>
      <div class="tutup-modal" @click="$emit('close')">
        <p>Tutup</p>
      </div>
      <div class="note">
        <p>* Harap menghubungi kontak yang tersedia</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    idGrup: {
      type: Number,
      default: 0,
    },
  },
};
</script>

<style scoped>
.modal-container {
  display: flex;
  flex-direction: column;
  gap: 5px;
  justify-content: center;
  align-items: center;
  position: fixed;
  z-index: 1;
  /* Sit on top */
  padding-top: 100px;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgb(0, 0, 0);
  background-color: rgba(0, 0, 0, 0.4);
}

.message-modal {
  width: 45%;
  background-color: #daeaf1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border-radius: 20px;
  padding: 15px;
  gap: 5px;
  border: 1px solid #888;
}

.fa-solid {
  margin-right: 10px;
}

.message-modal h1 {
  font-family: "Quicksand", sans-serif;
  font-size: 50px;
  color: red;
  margin-bottom: 20px;
}

.message-modal h2 {
  font-family: "Quicksand", sans-serif;
  font-weight: 800;
}

.message-modal h3 {
  font-family: "Quicksand", sans-serif;
  font-weight: 800;
  margin-bottom: 20px;
}

.message-modal p {
  font-family: "Quicksand", sans-serif;
  font-weight: 800;
}

.message-modal .id-grup-modal {
  font-size: 24px;
}

.message-modal .id-grup {
  font-size: 80px;
  margin-bottom: 10px;
}

.tutup-modal {
  background-color: white;
  font-weight: bold;
  text-align: center;
  color: black;
  padding: 10px;
  width: 100px;
  margin-bottom: 20px;
  border-radius: 10px;
}

.tutup-modal:hover {
  background-color: red;
  cursor: pointer;
  color: white;
}

.message-modal .note {
  font-style: italic;
}

@media only screen and (max-width: 729px) {
  .message-modal {
    width: 85%;
  }

  .message-modal h1 {
    font-size: 30px;
  }

  .message-modal h2 {
    font-size: 18px;
  }

  .message-modal h3 {
    font-size: 18px;
  }
}

@media only screen and (min-width: 730px) {
  .message-modal {
    width: 70%;
  }

  .message-modal h1 {
    font-size: 40px;
  }

  .message-modal h2 {
    font-size: 18px;
  }

  .message-modal h3 {
    font-size: 18px;
  }
}

@media only screen and (min-width: 900px) {
  .message-modal {
    width: 60%;
  }

  .message-modal h1 {
    font-size: 50px;
  }

  .message-modal h2 {
    font-family: "Quicksand", sans-serif;
    font-weight: 800;
    font-size: 25px;
  }

  .message-modal h3 {
    font-family: "Quicksand", sans-serif;
    font-weight: 800;
    font-size: 20px;
    margin-bottom: 20px;
  }
}

@media only screen and (min-width: 1024px) {
  .message-modal {
    width: 60%;
  }
}

@media only screen and (min-width: 1440px) {
  .message-modal {
    width: 45%;
  }
}
</style>
