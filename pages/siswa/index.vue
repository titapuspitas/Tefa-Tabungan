<template>
    <div class="container-fluid pe-3 pt-5 pb-3">
      <div class="row text-center p-2">
        <H1>DATA SISWA</H1>
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
                <td>id</td>
                <td>nis</td>
                <td>Nama</td>
                <td>Jenis kelamin</td>
                <td>Alamat</td>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(visitor,i) in visitors" :key="i">
              <td>{{ i+1 }}.</td>
              <td>{{ visitor.nis }}</td>
              <td>{{ visitor.nama }}</td>
              <td>{{ visitor.jenis_kelamin }}</td>
              <td>{{ visitor.alamat }}</td>
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
  const { data, error } = await supabase.from('siswa').select( `*`)
  .ilike('nama', `%${keyword.value}%`)
  if(data) visitors.value = data
}

onMounted(() => {
  getData()
})
</script>

<style scope>

</style>