<script setup>
import axios from 'axios';
import { onMounted, reactive } from 'vue';

const state = reactive({
  gempa: [],
  gempaBersih: [],
});


onMounted(()=>{
  getData();
})

function getData() {
  axios.get("https://data.bmkg.go.id/DataMKG/TEWS/autogempa.json").then((ress) => {
    console.log(ress);
    state.gempa = ress.data;
    state.gempaBersih = ress.data.Infogempa.gempa;
  })
}
</script>

<template>
  <div>
    <p>{{ state.gempa }}</p>
    <p>{{ state.gempa.Infogempa }}</p>
    <p>{{ state.gempaBersih }}</p>
    <!-- di bawah cara mendapat rincian -->
    <h2>Di sini jadi biasa, data yang di dalem state gempa atau state gemba bersih dibreakdown</h2>
    <p>{{ state.gempaBersih.Tanggal }}</p>
    <p>{{ state.gempaBersih.Jam }}</p>
    <p>Bisa juga pake judul. Misal <strong>Magnitude </strong>{{ state.gempaBersih.Magnitude }}</p>
    <p>{{ state.gempaBersih.Wilayah }}</p>
    <p class="merah">{{ state.gempaBersih.Potensi }}</p>
  </div>
</template>

<style scoped>
div {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.merah {
  color: red;
  font-size: 30px;
}
</style>
