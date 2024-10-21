<template>
  <div class="container-fluid pe-3 pt-5 pb-3">
    <div class="row text-center p-2">
        <h1>RIWAYAT SALDO</h1>
    </div>
    <form  @submit.prevent="getData"></form>
      <div class="row justify-content-center">
        <div class="col-12 p-3">
      <table class="table ">
      <thead>
        <tr>
          <th scope="col">id</th>
          <th scope="col">Nama</th>
          <th scope="col">Tanggal</th>
          <th scope="col">Masuk</th>
          <th scope="col">Keluar</th>
          <th scope="col">Saldo</th>
        </tr>
      </thead>
      <tbody>
              <tr v-for="(visitor,i) in visitors" :key="i">
              <td>{{ i+1 }}.</td>
              <td>{{ visitor.Nama }}</td>
              <td>{{ visitor.Tanggal }}</td>
              <td>{{ visitor.Masuk }}</td>
              <td>{{ visitor.Keluar }}</td>
              <td>{{ visitor.Saldo }}</td>
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
  const { data, error } = await supabase.from('riwayat').select( `*`).order('id')
  .ilike('nama', `%${keyword.value}%`)
  if(data) visitors.value = data
}

onMounted(() => {
  getData()
})
</script>