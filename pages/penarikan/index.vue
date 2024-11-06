<template>
  <div class="container-fluid p-5">
    <div class="row mb-5">
      <h1>TABUNGAN > PENARIKAN</h1>
    </div>
    <div class="row justify-content-end">
      <div class="col-5 p-3">
        <form @submit.prevent="getData">
          <input v-model="keyword" type="search" class="form-control" placeholder="Search ...">
        </form>
      </div>
    </div>
    <div class="row">
      <div class="col">
        <table class="table table-bordered">
          <thead>
            <tr>
              <th scope="col">ID</th>
              <th scope="col">WAKTU</th>
              <th scope="col">Nama</th>
              <th scope="col">Nominal</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(visitor, i) in filteredVisitors" :key="i">
              <td>{{ i + 1 }}.</td>
              <td>{{ visitor.tgl }}</td>
              <td>{{ visitor.siswa.nama }}</td>
              <td>{{ visitor.nominal }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';
const supabase = useSupabaseClient();
const keyword = ref('');
const visitors = ref([]);

// Fungsi untuk mengambil data
const getData = async () => {
  const { data } = await supabase
    .from('penarikan')
    .select('*, siswa(*)')
    .order('tgl', { ascending: false });
    
  if (data) visitors.value = data;
}

// Computed property untuk memfilter data berdasarkan kata kunci
const filteredVisitors = computed(() => {
  if (!keyword.value) return visitors.value; // Jika tidak ada kata kunci, kembalikan semua data
  return visitors.value.filter(visitor => {
    // Filter berdasarkan nama siswa dan nominal
    return visitor.siswa.nama.toLowerCase().includes(keyword.value.toLowerCase()) ||
          visitor.nominal.toString().includes(keyword.value);
  });
});

// Ambil data saat komponen dimuat
onMounted(() => {
  getData();
});
</script>

<style scoped>
.table {
  text-align: center;
}
.container-fluid {
  max-height: 85vh;
  overflow: auto;
}
</style>
