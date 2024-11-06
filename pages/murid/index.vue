<template>
  <div class="container-fluid">
    <div class="row justify-content-evenly">
      <div class="col-md-3 m-3 d-flex justify-content-end align-items-center profil text-center"><nuxt-link to="/identitas" class="test"> Profil <i class="ms-5 bi bi-person-fill zoom "></i></nuxt-link></div>
      <div class="col-md-3 m-3 d-flex justify-content-end align-items-center riwayat text-center"><nuxt-link to="/riwayats" class="test"> Saldo : {{ totalBalance.saldo }} <i class="ms-5 bi bi-pie-chart-fill zoom"></i></nuxt-link></div>
    </div>
  </div>
</template>

<!-- <script setup>
const user = useSupabaseUser()
console.log(user)
</script> -->

<style scope>
a{
  text-decoration: none;
}
.test{
  text-align: center;
  color: black;
}
  .zoom{
    font-size: 100px;
  }
  .profil{
    font-size: 30px;
    min-height: 150px;
    background-color: #BCDF5B;
  }
  .riwayat{
    font-size: 30px;
    background-color: #BF4E0E;
  }
</style>

<script setup>
const client = useSupabaseClient()
const totalBalance = ref(0)
const siswa = ref()
const user = useSupabaseUser()

const getProfile = async () => {
    const { data, error } = await client
    .from('profile')
    .select()
    .eq('user_id', user.value.id)
    .single()
    if(data) {
      siswa.value = data
    }
    
}

const fetchTotalBalance = async () => {
  // console.log(siswa.id)
  const { data, error } = await client
  .from('siswa')
  .select()
  .eq('id',siswa.value.id)
  .single();
  if (data) totalBalance.value = data
}
onMounted(() => {
  getProfile()
  setTimeout(() => {
    fetchTotalBalance()
  }, 1000);
})

</script>