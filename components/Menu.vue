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
        <li class="siswa mb-3 "><svg xmlns="http://www.w3.org/2000/svg"  fill="currentColor" class="bi bi-people" viewBox="0 0 16 16">
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
          <NuxtLink to="/pemasukan" style="color:white ; font-size: 20px;">
            <li class="pemasukan mb-3"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="biw bi-wallet2" viewBox="0 0 18 19">
  <path d="M12.136.326A1.5 1.5 0 0 1 14 1.78V3h.5A1.5 1.5 0 0 1 16 4.5v9a1.5 1.5 0 0 1-1.5 1.5h-13A1.5 1.5 0 0 1 0 13.5v-9a1.5 1.5 0 0 1 1.432-1.499zM5.562 3H13V1.78a.5.5 0 0 0-.621-.484zM1.5 4a.5.5 0 0 0-.5.5v9a.5.5 0 0 0 .5.5h13a.5.5 0 0 0 .5-.5v-9a.5.5 0 0 0-.5-.5z"/>
</svg>Pemasukan</li>
          </NuxtLink>
          <NuxtLink to="/penarikan" style="color:white ; font-size: 20px;">
            <li class="penarikan mb-3"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="biw bi-wallet2" viewBox="0 0 18 19">
  <path d="M12.136.326A1.5 1.5 0 0 1 14 1.78V3h.5A1.5 1.5 0 0 1 16 4.5v9a1.5 1.5 0 0 1-1.5 1.5h-13A1.5 1.5 0 0 1 0 13.5v-9a1.5 1.5 0 0 1 1.432-1.499zM5.562 3H13V1.78a.5.5 0 0 0-.621-.484zM1.5 4a.5.5 0 0 0-.5.5v9a.5.5 0 0 0 .5.5h13a.5.5 0 0 0 .5-.5v-9a.5.5 0 0 0-.5-.5z"/>
</svg>Penarikan</li>
          </NuxtLink>

      </span>

      <span v-else>
        <NuxtLink to="/murid">
        <li class="beranda mb-3"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi-house bi-house-door-fill" viewBox="0 0 18 18">
          <path d="M6.5 14.5v-3.505c0-.245.25-.495.5-.495h2c.25 0 .5.25.5.5v3.5a.5.5 0 0 0 .5.5h4a.5.5 0 0 0 .5-.5v-7a.5.5 0 0 0-.146-.354L13 5.793V2.5a.5.5 0 0 0-.5-.5h-1a.5.5 0 0 0-.5.5v1.293L8.354 1.146a.5.5 0 0 0-.708 0l-6 6A.5.5 0 0 0 1.5 7.5v7a.5.5 0 0 0 .5.5h4a.5.5 0 0 0 .5-.5"/>     
          </svg>Beranda
        </li>
      </NuxtLink>
      <NuxtLink to="/identitas">
        <li class="beranda mb-3"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-people" viewBox="0 0 16 16">
  <path d="M15 14s1 0 1-1-1-4-5-4-5 3-5 4 1 1 1 1zm-7.978-1L7 12.996c.001-.264.167-1.03.76-1.72C8.312 10.629 9.282 10 11 10c1.717 0 2.687.63 3.24 1.276.593.69.758 1.457.76 1.72l-.008.002-.014.002zM11 7a2 2 0 1 0 0-4 2 2 0 0 0 0 4m3-2a3 3 0 1 1-6 0 3 3 0 0 1 6 0M6.936 9.28a6 6 0 0 0-1.23-.247A7 7 0 0 0 5 9c-4 0-5 3-5 4q0 1 1 1h4.216A2.24 2.24 0 0 1 5 13c0-1.01.377-2.042 1.09-2.904.243-.294.526-.569.846-.816M4.92 10A5.5 5.5 0 0 0 4 13H1c0-.26.164-1.03.76-1.724.545-.636 1.492-1.256 3.16-1.275ZM1.5 5.5a3 3 0 1 1 6 0 3 3 0 0 1-6 0m3-2a2 2 0 1 0 0 4 2 2 0 0 0 0-4"/>
</svg>Profil
        </li>
      </NuxtLink>
      <NuxtLink to="/riwayats">
        <li class="beranda mb-3"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-bookmarks-fill" viewBox="0 0 17 17">
  <path d="M2 4a2 2 0 0 1 2-2h6a2 2 0 0 1 2 2v11.5a.5.5 0 0 1-.777.416L7 13.101l-4.223 2.815A.5.5 0 0 1 2 15.5z"/>
  <path d="M4.268 1A2 2 0 0 1 6 0h6a2 2 0 0 1 2 2v11.5a.5.5 0 0 1-.777.416L13 13.768V2a1 1 0 0 0-1-1z"/>
</svg>Riwayat
        </li>
      </NuxtLink>
</span>
      <NuxtLink to="/logout" style="color:white ; font-size: 20px;">
        <li class="logout mb-3"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi1 bi-box-arrow-in-left" viewBox="0 0 15 15">
  <path fill-rule="evenodd" d="M10 3.5a.5.5 0 0 0-.5-.5h-8a.5.5 0 0 0-.5.5v9a.5.5 0 0 0 .5.5h8a.5.5 0 0 0 .5-.5v-2a.5.5 0 0 1 1 0v2A1.5 1.5 0 0 1 9.5 14h-8A1.5 1.5 0 0 1 0 12.5v-9A1.5 1.5 0 0 1 1.5 2h8A1.5 1.5 0 0 1 11 3.5v2a.5.5 0 0 1-1 0z"/>
  <path fill-rule="evenodd" d="M4.146 8.354a.5.5 0 0 1 0-.708l3-3a.5.5 0 1 1 .708.708L5.707 7.5H14.5a.5.5 0 0 1 0 1H5.707l2.147 2.146a.5.5 0 0 1-.708.708z"/>
</svg>
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
  background-size: 45px;
  font-size: 20px;
  color: white;
  font-size: 20px;
  color: white;
}
.siswa{
  padding-left: 20px;
  background-size: 45px;
  font-size: 20px;
  color: white;
  font-size: 20px;
  color: white;
}
.tabungan{
  padding-left: 20px;
  background-size: 45px;
  font-size: 20px;
  color: white;
  color: white;
  font-size: 20px;
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
.bi1{
  margin-right: 25px;
  padding-right: 1px;
  margin-left: 25px;
  width:25px;
  height: 25px;
  background-size: 40px;
  font-size: 20px;
}
.biw{
  margin-right: 25px;
  padding-right: 1px;
  margin-left: 25px;
  width:25px;
  height: 25px;
  background-size: 35px;
  font-size: 20px;
  color: white;
  font-size: 20px;


}




</style>
