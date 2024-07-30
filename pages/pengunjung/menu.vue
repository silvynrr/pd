<template>
  <div class="content">
    <div class="container-fluid d-flex justify-content-around">
      <div class="row mx-1 py-5">
        <div class="col-lg-6 col mb-3">
          <nuxt-link to="/pengunjung/riwayat">
            <div class="card bg-pengunjung rounded-5" style="height: 85vh; ">
              <div class="card-body pt-5">
                <h2 class="text-center" style="margin-top: 350px;">RIWAYAT KUNJUNGAN</h2>
              </div>
            </div>
          </nuxt-link>
        </div>

        <div class="col-lg-6 col">
          <nuxt-link to="/buku">
            <div class="card bg-buku rounded-5" style="height: 85vh; padding: 0px 80px;">
              <div class="card-body pt-5">
                <h2 class="text-center" style="margin-top: 350px;">CARI BUKU</h2>
              </div>
            </div>
          </nuxt-link>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
.content{
  background-color: #6AB187;
  /* height: 100vh; */
  width: 100%;
}
.card {
  opacity: 85%;
  color: white;
  align-items: center;
  height:250px;
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
</style>
