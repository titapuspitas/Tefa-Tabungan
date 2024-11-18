<template>
  <div class="container-fluid p-5">
    <h2 class="text-start my-4 p-3">{{ siswa?.fullname }}</h2>
      <div class="col-md-12">
        <ul class="list-group list-group-flush p-3">
          <li v-if="siswa" class="list-group-item p-3 m-1">id : {{ siswa?.id }}</li>
          <li v-if="siswa" class="list-group-item p-3 m-1">Nis : {{ siswa?.Nis }}</li>
          <li v-if="siswa" class="list-group-item p-3 m-1">Alamat : {{ siswa?.alamat }}</li>
          <li v-if="siswa" class="list-group-item p-3 m-1">Jenis Kelamin : {{ siswa?.jenis_kelamin }}</li>
          <span v-else class="p-3">sedang memuat...</span>
        </ul>
      </div>
  </div>
</template>

<script setup>

const supabase = useSupabaseClient()
const siswa = ref()
const user = useSupabaseUser()

const getProfile = async () => {
    const { data, error } = await supabase
    .from('profile')
    .select()
    .eq('user_id', user.value.id)
    .single()
    if(data) siswa.value = data
}

onMounted(() => {
  getProfile()
})
</script>

<style scoped>
.container-fluid {
  background-color: #f4f4f4;
  border-radius: 12px;
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
  padding: 30px;
}

.list-group-item {
  background-color: #fff;
  border-radius: 10px;
  padding: 20px;
  font-size: 1.1rem;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  transition: box-shadow 0.3s ease-in-out;
}
</style>
