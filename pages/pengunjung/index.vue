<template>
  <div div class="content">
    <div class="container-fluid">
      <div class="row">
        <div class="col-lg-12">
          <form @submit.prevent="kirimData">
            <h2 class="text-center my-4">ISI DATA KUNJUNGAN</h2>
            <div class="mb-3">
              <input v-model="form.nama" type="text" class="form-control form-control-lg rounded-5"
                placeholder="Nama...">
            </div>

            <div class="mb-3">
              <select v-model="form.keanggotaan" @change="resetKelas"
                class="form-control form-control-lg form-select rounded-5">
                <option value="">Keanggotaan...</option>
                <option v-for="(member, i) in members" :key="i" :value="member.id">{{ member.nama }}</option>
              </select>
            </div>

            <div v-if="form.keanggotaan == '2'" class="mb-3">
              <div class="row">
                <div class="col-md-4">
                  <select v-model="form.tingkat" class="form-control form-control-lg form-select rounded-5 mb-2">
                    <option value="">Tingkat...</option>
                    <option value="X">X</option>
                    <option value="XI">XI</option>
                    <option value="XII">XII</option>
                  </select>
                </div>

                <div class="col-md-4">
                  <select v-model="form.jurusan" class="form-control form-control-lg form-select rounded-5 mb-2">
                    <option value="">Jurusan...</option>
                    <option value="PPLG">PPLG</option>
                    <option value="TJKT">TJKT</option>
                    <option value="TSM">TSM</option>
                    <option value="DKV">DKV</option>
                    <option value="TOI">TOI</option>
                  </select>
                </div>

                <div class="col-md-4">
                  <select v-model="form.kelas" class="form-control form-control-lg form-select rounded-5 mb-2">
                    <option value="">Kelas...</option>
                    <option value="1">1</option>
                    <option value="2">2</option>
                    <option value="3">3</option>
                    <option value="4">4</option>
                  </select>
                </div>
              </div>
            </div>
            <div class="mb-3">
              <select v-model="form.keperluan" class="form-control form-control-lg form-select rounded-5">
                <option value="">Keperluan...</option>
                <option v-for="(item, i) in objectives" :key="i" :value="item.id">{{ item.nama }}</option>
              </select>
            </div>
            <input type="submit" class="btn btn-light rounded-5 px-5"></input>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient()

const members = ref([])
const objectives = ref([])
const form = ref({
  nama: "",
  keanggotaan: "",
  tingkat: "",
  jurusan: "",
  kelas: "",
  keperluan: ""
})
const kirimData = async () => {
  const { error } = await supabase.from('Pengunjung').insert([form.value])
  if (error) throw error
  else navigateTo('/pengunjung/riwayat')
}
const getKeanggotaan = async () => {
  const { data, error } = await supabase.from('Keanggotaan').select('*')
  if (data) members.value = data
}
const getKeperluan = async () => {
  const { data, error } = await supabase.from('Keperluan').select('*')
  if (data) objectives.value = data
}
const resetKelas = e => {
  if (e.target.value === '2' || '3' || '4') {
    form.value.tingkat = ''
    form.value.jurusan = ''
    form.value.kelas = ''
  }
}
onMounted(() => {
  getKeanggotaan()
  getKeperluan()
})
</script>

<style scoped>
.content {
  background-color: #235C4E;
  height: 100vh;
  width: 100%;
}

.container-fluid {
  width: 100%;
  height: 500px;
  padding-top: 150px;
}

.btn {
  /* font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif; */
  background-color: rgb(255, 255, 255);
  color: black;
  width: 150px;
  height: 50px;
}

form {
  /* background-color: #20948B; */
  width: 100%;
  border-radius: 20px;
  font-family: '';
  color: white;

}

::placeholder {
  color: rgba(0, 0, 0, 0.788);
  font-size: large;
}
</style>