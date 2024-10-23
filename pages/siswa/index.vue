<template>
    <div class="container-fluid pe-3 pt-5 pb-3">
      <div class="row text-center p-2">
        <h1>DATA SISWA</h1>
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
                <th scope="col">Id</th>
                <th scope="col">Nis</th>
                <th scope="col">Nama</th>
                <th scope="col">Jenis Kelamin</th>
                <th scope="col">Alamat</th>
                <th scope="col">Saldo</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(visitor,i) in visitors" :key="i">
              <td>{{ i+1 }}.</td>
              <td>{{ visitor.nis }}</td>
              <td>{{ visitor.nama }}</td>
              <td>{{ visitor.jenis_kelamin }}</td>
              <td>{{ visitor.alamat }}</td>
              <td>{{ visitor.saldo }}</td>
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
const data = ref(visitors)

const getData = async () => {
  const { data, error } = await supabase.from('siswa').select( `*`).order('id')
  .ilike('nama', `%${keyword.value}%`)
  if(data) visitors.value = data
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