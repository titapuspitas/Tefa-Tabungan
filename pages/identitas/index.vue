<template>
  <div>
    <h2 class="text-start my-4">{{ siswa.nama }}</h2>
      <div class="col-md-12">
        <ul class="list-group list-group-flush">
          <li class="list-group-item">id : {{  siswa.id }}</li>
          <li class="list-group-item">nis : {{  siswa.nis }}</li>
          <li class="list-group-item">nama : {{ siswa.nama }}</li>
          <li class=" list-group-item">jenis_kelamin : {{ siswa.jenis_kelamin }}</li>
          <li class=" list-group-item">alamat : {{ siswa.alamat }}</li>
        </ul>
      </div>
  </div>
</template>

<script setup>

const supabase = useSupabaseClient()
const siswa = ref([])

const getSiswaById = async () => {
    const { data, error } = await supabase
    .from('siswa')
    .select(`*`)
    if(data) siswa.value = data
}

onMounted(() => {
    getSiswaByID()
})
</script>