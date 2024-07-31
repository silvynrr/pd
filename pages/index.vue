<template>
  <div class="content">
    <div class="container-fluid">
      <div class="row mx-1 py-5">
        <div class="col-lg-6 col-12 mb-3">
          <nuxt-link to="/pengunjung/riwayat" class="text-black text-decoration-none">
            <div class="card bg-pengunjung rounded-5">
              <div class="card-body pt-5">
                <h2 class="text-center text-white mt-5">RIWAYAT KUNJUNGAN</h2>
              </div>
            </div>
          </nuxt-link>
        </div>

        <div class="col-lg-6 col-12">
          <nuxt-link to="/buku" class="text-black text-decoration-none">
            <div class="card bg-buku rounded-5">
              <div class="card-body pt-5">
                <h2 class="text-center text-white mt-5">CARI BUKU</h2>
              </div>
            </div>
          </nuxt-link>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <h2>Statistik</h2>
        </div>
      </div>
      <div class="row gy-3">
        <div class="col-12 col-lg-6">
          <div class="card pengunjung rounded-5">
            <div class="card-body">
              <h2 class="text-center mt-5">{{ jmlPengunjung }} pengunjung</h2>
            </div>
          </div>
        </div>
        <div class="col-12 col-lg-6">
          <div class="card buku rounded-5">
            <div class="card-body">
              <h2 class="text-center mt-5">{{ jmlBuku }}Buku</h2>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient()
const jmlPengunjung = ref(0)
const jmlBuku = ref(0)

async function getJmlPengunjung() {
  const { data, count } = await supabase.from("Pengunjung")
    .select('*', { count: "exact" })
  if (data) jmlPengunjung.value = count
}

async function getJmlBuku() {
  const { data, count } = await supabase.from("Buku")
    .select('*', { count: "exact" })
  if (data) jmlBuku.value = count
}
onMounted(() => {
  getJmlPengunjung()
  getJmlBuku()
})
</script>
<style scoped>
.content {
  background-color: #ffffff;
  /* height: 100vh; */
  width: 100%;
}

.card {
  opacity: 85%;
  align-items: center;
  height: 250px;
}

.card.bg-pengunjung {
  background-image: url('@/assets/img/bg-home-kunjungan.jpg');
  background-repeat: no-repeat;
  background-position: center center;
  background-size: cover;
}

.card.bg-buku {
  background: url('@/assets/img/bg-home-cari-buku.jpg');
  background-size: cover;
}

.card.pengunjung {
  /* warna card statistik pengunjung */
  background-color: #ffff00;
}

.card.buku {
  /* warna card statistik buku */
  background-color: #6da2ac;
}
</style>
