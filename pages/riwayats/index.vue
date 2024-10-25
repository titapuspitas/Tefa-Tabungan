<template>
  <div class="container-fluid pe-3 pt-5 pb-3">
    <div class="row text-center p-2">
      <ul class="nav">
  <li class="nav-item" >
    <a class="nav-link active" aria-current="page" href="#">Pemasukan</a>
  </li>
  <li class="nav-item">
    <a class="nav-link" href="#">Pengeluaran</a>
  </li>
</ul>
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

<style scoped>
.nav{
  padding-top: 0;
  font-size: 150%;

}
</style>

