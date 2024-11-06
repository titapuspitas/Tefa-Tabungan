<template>
  <div class="container-fluid">
    <div class="row justify-content-evenly">
      <div v-if="userRole == 'guru'" class="col-md-3 m-3 d-flex justify-content-end align-items-center siswaa text-center "><nuxt-link to="/siswa" class="test">Siswa<i class="ms-5 bi bi-person-fill zoom "></i></nuxt-link></div>
      <div v-if="userRole == 'guru'" class="col-md-3 m-3 d-flex justify-content-end align-items-center tabungann text-center"><nuxt-link to="/tabungan" class="test">Tabungan<i class="ms-4 bi bi-bar-chart-fill zoom"></i></nuxt-link></div>
      <div v-if="userRole == 'siswa'" class="col-md-3 m-3 d-flex justify-content-end align-items-center siswaa text-center "><nuxt-link to="/siswa" class="test">profil<i class="ms-5 bi bi-person-fill zoom "></i></nuxt-link></div>
      <div v-if="userRole == 'guru'"  class="col-md-3 m-3 d-flex justify-content-end align-items-center saldo text-center"><nuxt-link to="/rekapan" class="test">{{ totalBalance.saldo_semua }}<i class="ms-5 bi bi-pie-chart-fill zoom "></i></nuxt-link></div>
      <div v-if="userRole == 'siswa'" class="col-md-3 m-3 d-flex justify-content-end align-items-center saldo text-center "><nuxt-link to="/siswa" class="test">Saldo<i class="ms-5 bi bi-pie-chart-fill zoom"></i></nuxt-link></div>
    </div>
  </div>
</template>

<script setup>
const client = useSupabaseClient()
const user = useSupabaseUser()
const userRole = ref('')
const totalBalance = ref(0);


async function getRole() {
  let { data, error } = await client
    .from('profile')
    .select('role')
    .eq('user_id', user.value.id)
    .single()
  if(error) throw error
  if(data) userRole.value = data.role
}

const fetchTotalBalance = async () => {
  const { data, error } = await client
  .from('jumlah_tabungan')
  .select()
  .single();
  if (data) totalBalance.value = data

  if (error) {
    console.log('Fetched data:', data);
  //  totalBalance.value = data.reduce((acc, jumlah_tabungan) => acc + jumlah_tabungan.saldo_semua, 0);
  }

// return {
//   totalBalance,
// };
}



onMounted(() => {
  getRole()
  fetchTotalBalance()
})
</script>

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
  .siswaa{
    font-size: 30px;
    min-height: 150px;
    background-color: #BCDF5B;
  }
  .tabungann{
    font-size: 30px;
    background-color: #5E99CF;
  }
  .saldo{
    font-size: 30px;
    background-color: #BF4E0E;
  }
</style>