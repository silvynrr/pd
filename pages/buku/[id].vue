<template>
  <div class="content">
    <div class="container-fluid pt-5">
      <h2 class="text-center text-white">RINCIAN BUKU</h2>
      <div class="row d-flex justify-content-center flex-md-wrap">
        <div class="col-auto col-lg-3 ">
          <img :src="buku?.cover" alt="cover buku" style="width: 250px;">
        </div>
        <div class="col-8 text-white">
          <div class="row">
            <h1 class="text start text-center my-4">{{ buku?.judul }}</h1>
          </div>
          <div class="row">
            <h2>PENULIS: {{ buku?.penulis }}</h2>
            <h2>PENERBIT: {{ buku?.penerbit }}</h2>
            <h2>TAHUN TERBIT: {{ buku?.tahun_terbit }}</h2>
            <h2>RAK: {{ buku?.rak }}</h2>
            <h2>KATEGORI: {{ buku?.kategori_buku?.nama }}</h2>
            <h2>DESKRIPSI: {{ buku?.deskripsi }}</h2>
          </div>
        </div>
      </div>
      <div class="row d-flex justify-content-center mt-4">
        <nuxt-link to="/buku" class="col-1 btn btn-dark btn-lg rounded-5 text-center">Kembali</nuxt-link>
      </div>
    </div>
  </div>
</template>
<script setup>
import { onMounted } from 'vue';

const supabase = useSupabaseClient()
const route = useRoute()
const buku = ref()
const kategories = ref([])

const getBookByid = async () => {
  const { data, error } = await supabase
    .from('Buku')
    .select(`*, kategori_buku(*)`)
    .eq('id', route.params.id)
    .maybeSingle()
  if (error) throw error
  if (data) buku.value = data
}

const getKategori = async () => {
  const { data, error } = await supabase
    .from('kategori_buku')
    .select('*')
  if (data) kategories.value = data
}


onMounted(() => {
  getBookByid()
  getKategori()
})

</script>
<style scoped>
.content {
  background-color: #6AB187;
  background-size: cover;
  width: 100%;
  /* height: 100vh; */
  font-family: '';
  color: black;
}

.btn {
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  background-color: rgb(255, 255, 255);
  color: black;
  width: 160px;
  height: 50px;
}
</style>