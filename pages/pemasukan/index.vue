<template>
  <div class="container-fluid p-5">
    <div class="row mb-5">
      <H1>TABUNGAN > PEMASUKAN</H1>
      </div>
      <div class="row justify-content-end">
        <div class="col-5 p-3">
          <form  @submit.prevent="getData">
            <input v-model="keyword" type="search" class="form-control" placeholder="Search ...">
          </form>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <table class="table table-bordered">
            <thead>
            <tr>
              <th scope="col">id</th>
              <th scope="col">WAKTU</th>
              <th scope="col">Nama</th>
              <th scope="col">nominal</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(visitor,i) in visitors" :key="i">
              <td>{{ i+1 }}.</td>
              <td>{{ visitor.tgl }}</td>
              <td>{{ visitor.siswa.nama }}</td>
              <td>{{ visitor.nominal }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>
<script setup>
const supabase = useSupabaseClient()
const keyword = ref('')
const visitors = ref([])

const getData = async () => {
  const { data } = await supabase
  .from('pemasukan')
  .select('*, siswa(*)')
  .order('tgl',  { ascending: false });
  if(data) visitors.value = data;
}

onMounted(() => {
  getData()
})
</script>

<style scoped>
.table{
  text-align: center;
}
.container-fluid{
  max-height: 85vh;
  overflow: auto;
}
</style>