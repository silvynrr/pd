<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-lg-12">
        <h2 class="text-center my-4">RIWAYAT KUNJUNGAN</h2>
        <div class="my-3">menampilkan {{ visitors?.length }} dari {{ totalVisitors }}</div>
        <div class="table-responsive">
          <table class="table table-bordered border-white text-white">
            <thead>
              <tr>
                <td>#</td>
                <td>Tanggal</td>
                <td>Waktu</td>
                <td>Nama</td>
                <td>Keanggotaan</td>
                <td>Kelas</td>
                <td>Keperluan</td>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(visitor, i) in visitors" :key="i">
                <td>{{ i + 1 }}.</td>
                <td>{{ visitor.tanggal }}</td>
                <td>{{ visitor.waktu }}</td>
                <td>{{ visitor.nama }}</td>
                <td>{{ visitor.keanggotaan.nama }}</td>
                <td>{{ visitor.tingkat }}-{{ visitor.jurusan }}{{ visitor.kelas }}</td>
                <td>{{ visitor.keperluan.nama }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
    <div class="row justify-content-between">
      <div class="col-auto">
        <nuxt-link to="/" class="btn btn-dark rounded-5">Menu</nuxt-link>
      </div>
      <div class="col-auto">
        <nuxt-link to="/pengunjung" class="btn btn-dark rounded-5">Isi Kunjungan</nuxt-link>
      </div>
    </div>
  </div>
</template>
<script setup>
const supabase = useSupabaseClient()

const visitors = ref([])
const totalVisitors = ref(0)
const getPengunjung = async () => {
  const { data, error } = await supabase.from('Pengunjung').select(`*, keanggotaan(*), keperluan(*)`)
  if (error) throw error
  if (data) visitors.value = data
}
const getTotalPengunjung = async () => {
  const { count, error } = await supabase.from('Pengunjung').select('*', { count: 'exact', head: true })
  if (error) throw error
  if (count) totalVisitors.value = count
}
onMounted(() => {
  getPengunjung()
  getTotalPengunjung()
})
</script>

<style scoped>
.container-fluid {
  background: #235C4E;
  background-size: cover;
  /* height: 100vh; */
  width: 100%;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  color: rgb(0, 0, 0);
  color: rgb(255, 255, 255);
  opacity: 70%;
}

.btn {
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  background-color: rgb(243, 243, 243);
  color: rgb(0, 0, 0);
  width: 150px;
  height: 50px;
}

.table td {
  background: #235C4E;
  color: rgb(255, 255, 255);
}
</style>