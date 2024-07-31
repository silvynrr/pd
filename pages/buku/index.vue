<template>
  <div class="wrapper">
    <div class="content"></div>
    <div class="container-fluid">
      <div class="row">
        <div class="col-lg-12">
          <h2 class="text-center my-4 text-white">CARI BUKU</h2>
          <form @submit.prevent="getBooks" class="col mb-3">
            <div class="input-group flex-nowrap rounded">
              <input v-model="keyword" type="search" class="form-control from-control-lg rounded-5"
                placeholder="Cari..." aria-label="Search" @input="getbooks" />
            </div>
          </form>
          <div class="my-3 text-white">menampilkan {{ books.length }} buku dari {{ books.length }}</div>
        </div>
      </div>
      <div class="row">
        <div v-for="(book, i) in books" :key="i" class="col-6 col-lg-3 mb-3">
          <div class="card">
            <nuxt-link :to="`/buku/${book.id}`">
              <div class="card-body">
                <img :src="book.cover" class="card-img-top" alt="cover">
              </div>
            </nuxt-link>
          </div>
        </div>
        <div class="row d-flex justify-content-end">
          <nuxt-link to="/pengunjung" class="col-1 btn btn-dark btn-lg rounded-5 px-5">menu</nuxt-link>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
const supabase = useSupabaseClient()

const keyword = ref('')
const books = ref([])

const getbooks = async () => {
  const { data, error } = await supabase
    .from('Buku')
    .select(`*, kategori(*)`)
    .ilike("judul", `%${keyword.value}%`)
    .order('id')
  if (data) books.value = data
}

onMounted(() => {
  getbooks()
})
</script>
<style scoped>
.content {
  background-color: #235C4E;
  background-size: cover;
  background-repeat: no-repeat;
  /* font-family: "Jockey One"; */
  position: fixed;
  top: 0;
  background-position: center;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: -1;

}

.card {
  /* width: 260px;
  height: 100%; */
  padding: 0;
}

.btn {
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  background-color: rgb(248, 246, 246);
  color: black;
  width: 150px;
  height: 50px;
}
</style>