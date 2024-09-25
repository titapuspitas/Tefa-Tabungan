<template>
  <div class="container-fluid p-5">
    <div class="row mb-5">
      <H1>TABUNGAN > PENARIKAN</H1>
    </div>
      <div class="row justify-content-end">
        <div class="col-5 p-3">
          <form  @submit.prevent="getData">
            <input v-model="keyword" type="search" class="form-control" placeholder="Search...">
          </form>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <table class="table table-bordered">
            <thead>
            <tr>
              <td>#</td>
              <td>WAKTU</td>
              <td>Nama</td>
              <td>nominal</td>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(visitor,i) in visitors" :key="i">
              <td>{{ i+1 }}.</td>
              <td>{{ visitor.tanggal }}, {{ visitor.waktu }}</td>
              <td>{{ visitor.Nama }}</td>
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
const data = ref(visitors)

const getData = async () => {
  const { data, error } = await supabase.from('pemasukan').select( `*`)
  .ilike('nama', `%${keyword.value}%`)
  if(data) visitors.value = data
}

onMounted(() => {
  getData()
})
</script>