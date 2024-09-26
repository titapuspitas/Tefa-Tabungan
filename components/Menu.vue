<template>
  <div class="p-0">
    <ul class="menu nav flex-column">
      <span v-if="profile.role == 'guru'">
      <NuxtLink to="/dashboard">
        <li class="beranda mb-3"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi-house bi-house-door-fill" viewBox="0 0 16 18">
          <path d="M6.5 14.5v-3.505c0-.245.25-.495.5-.495h2c.25 0 .5.25.5.5v3.5a.5.5 0 0 0 .5.5h4a.5.5 0 0 0 .5-.5v-7a.5.5 0 0 0-.146-.354L13 5.793V2.5a.5.5 0 0 0-.5-.5h-1a.5.5 0 0 0-.5.5v1.293L8.354 1.146a.5.5 0 0 0-.708 0l-6 6A.5.5 0 0 0 1.5 7.5v7a.5.5 0 0 0 .5.5h4a.5.5 0 0 0 .5-.5"/>     
          </svg>Beranda
        </li>
      </NuxtLink>
      <NuxtLink to="/siswa">
        <li class="siswa mb-3 "><svg xmlns="http://www.w3.org/2000/svg"  fill="currentColor" class="bi bi-people" viewBox="0 0 16 18">
          <path d="M15 14s1 0 1-1-1-4-5-4-5 3-5 4 1 1 1 1zm-7.978-1L7 12.996c.001-.264.167-1.03.76-1.72C8.312 10.629 9.282 10 11 10c1.717 0 2.687.63 3.24 1.276.593.69.758 1.457.76 1.72l-.008.002-.014.002zM11 7a2 2 0 1 0 0-4 2 2 0 0 0 0 4m3-2a3 3 0 1 1-6 0 3 3 0 0 1 6 0M6.936 9.28a6 6 0 0 0-1.23-.247A7 7 0 0 0 5 9c-4 0-5 3-5 4q0 1 1 1h4.216A2.24 2.24 0 0 1 5 13c0-1.01.377-2.042 1.09-2.904.243-.294.526-.569.846-.816M4.92 10A5.5 5.5 0 0 0 4 13H1c0-.26.164-1.03.76-1.724.545-.636 1.492-1.256 3.16-1.275ZM1.5 5.5a3 3 0 1 1 6 0 3 3 0 0 1-6 0m3-2a2 2 0 1 0 0 4 2 2 0 0 0 0-4"/>
          </svg>Siswa
        </li>
      </NuxtLink>
      <NuxtLink to="/tabungan">
        <li class="tabungan mb-3"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi-book bi-bookmarks-fill" viewBox="0 0 16 17">
          <path d="M2 4a2 2 0 0 1 2-2h6a2 2 0 0 1 2 2v11.5a.5.5 0 0 1-.777.416L7 13.101l-4.223 2.815A.5.5 0 0 1 2 15.5z"/>
          <path d="M4.268 1A2 2 0 0 1 6 0h6a2 2 0 0 1 2 2v11.5a.5.5 0 0 1-.777.416L13 13.768V2a1 1 0 0 0-1-1z"/>
        </svg>Tabungan
        </li>
      </NuxtLink>
        <ul>
          <NuxtLink to="/pemasukan/" style="text-decoration: none;color: white;">
            <li>Pemasukan</li>
          </NuxtLink>
          <NuxtLink to="/penarikan" style="text-decoration: none;color: white;">
            <li>Penarikan</li>
          </NuxtLink>
        </ul>
      </span>
<!-- 
      <span v-else>
        <NuxtLink to="/dashboard">
        <li class="beranda mb-3"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi-house bi-house-door-fill" viewBox="0 0 16 18">
          <path d="M6.5 14.5v-3.505c0-.245.25-.495.5-.495h2c.25 0 .5.25.5.5v3.5a.5.5 0 0 0 .5.5h4a.5.5 0 0 0 .5-.5v-7a.5.5 0 0 0-.146-.354L13 5.793V2.5a.5.5 0 0 0-.5-.5h-1a.5.5 0 0 0-.5.5v1.293L8.354 1.146a.5.5 0 0 0-.708 0l-6 6A.5.5 0 0 0 1.5 7.5v7a.5.5 0 0 0 .5.5h4a.5.5 0 0 0 .5-.5"/>     
          </svg>Beranda
        </li>
      </NuxtLink>
      <NuxtLink to="/profil">
        <li class="profil mb-3 "><svg xmlns="http://www.w3.org/2000/svg"  fill="currentColor" class="bi bi-people" viewBox="0 0 16 18">
          <path d="M15 14s1 0 1-1-1-4-5-4-5 3-5 4 1 1 1 1zm-7.978-1L7 12.996c.001-.264.167-1.03.76-1.72C8.312 10.629 9.282 10 11 10c1.717 0 2.687.63 3.24 1.276.593.69.758 1.457.76 1.72l-.008.002-.014.002zM11 7a2 2 0 1 0 0-4 2 2 0 0 0 0 4m3-2a3 3 0 1 1-6 0 3 3 0 0 1 6 0M6.936 9.28a6 6 0 0 0-1.23-.247A7 7 0 0 0 5 9c-4 0-5 3-5 4q0 1 1 1h4.216A2.24 2.24 0 0 1 5 13c0-1.01.377-2.042 1.09-2.904.243-.294.526-.569.846-.816M4.92 10A5.5 5.5 0 0 0 4 13H1c0-.26.164-1.03.76-1.724.545-.636 1.492-1.256 3.16-1.275ZM1.5 5.5a3 3 0 1 1 6 0 3 3 0 0 1-6 0m3-2a2 2 0 1 0 0 4 2 2 0 0 0 0-4"/>
          </svg>Profil
        </li>
      </NuxtLink>
      <NuxtLink to="/Saldo">
        <li class="saldo mb-3"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi-book bi-bookmarks-fill" viewBox="0 0 16 17">
          <path d="M2 4a2 2 0 0 1 2-2h6a2 2 0 0 1 2 2v11.5a.5.5 0 0 1-.777.416L7 13.101l-4.223 2.815A.5.5 0 0 1 2 15.5z"/>
          <path d="M4.268 1A2 2 0 0 1 6 0h6a2 2 0 0 1 2 2v11.5a.5.5 0 0 1-.777.416L13 13.768V2a1 1 0 0 0-1-1z"/>
        </svg>Saldo
        </li>
      </NuxtLink>
      </span> -->

      <NuxtLink to="/logout" class="text-white">
        <li class="logout mb-3">
          Logout
        </li>
      </NuxtLink>
    </ul>
  </div>
</template>


<script setup>
const user = useSupabaseUser()
const client = useSupabaseClient()
const profile = ref({
  user_id: "",
  role: "",
  fullname: ""
})

async function getRole() {
  let { data, error } = await client
    .from('profile')
    .select('*')
    .eq('user_id', user.value.id)
    .single()
  if(data) profile.value = data
}

onMounted(() => {
  getRole()
})
</script>



<style scoped>
a{
  text-decoration: none;
}
.menu{
  background: #3E3434;
  min-height: 85vh;
  width: 300px;
}
.beranda{
  margin-top: 30px;
  padding-left: 20px;
  background-size: 25px;
  font-size: 15px;
  color: white;
  font-size: 20px;
  color: white;
}
.siswa{
  padding-left: 20px;
  background-size: 25px;
  font-size: 15px;
  color: white;
  font-size: 20px;
  color: white;
}
.tabungan{
  padding-left: 20px;
  background-size: 25px;
  font-size: 25px;
  color: white;
  font-size: 20px;
  color: white;
}
.bi{
  padding-right: 1px;
  margin-right: 25px;
  width:25px;
  height: 25px;
}
.bi-house{
  padding-right: 1px;
  margin-right: 25px;
  width:25px;
  height: 25px;
}
.bi-book{
  padding-right: 1px;
  margin-right: 25px;
  width:25px;
  height: 25px;
}



</style>
