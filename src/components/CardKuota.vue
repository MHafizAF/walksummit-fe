<script setup>
const props = defineProps(["item"]);
</script>

<template>
  <div>
    <div class="card-jalur">
      <h2 tabindex="0">{{ item.nama }}</h2>
      <h3 tabindex="0">
        Sisa Kuota Hari ini :
        <i class="fa-solid fa-person-hiking"></i>{{ item.kuota }}
      </h3>
    </div>
  </div>
</template>

<style scoped lang="scss">
.content {
  display: flex;
  flex-direction: column;
  gap: 20px;
}
.card-jalur {
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
h2,
h3 {
  font-family: "Quicksand", sans-serif;
}
</style>
