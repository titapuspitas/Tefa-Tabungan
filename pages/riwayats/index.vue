<template>
  <div class="container-fluid">
    <div class="row justify-content-evenly">
      <div class="col-md-3 m-5 text-center">
        <div class="balance-box">
          <h4>Total Pemasukan</h4>
          <h5>{{ totalPemasukan.toLocaleString("id-ID", { style: "currency", currency: "IDR" }) }}</h5>
        </div>
      </div>
      <div class="col-md-3 m-5 text-center">
        <div class="balance-box">
          <h4>Total Penarikan</h4>
          <h5>{{ totalPenarikan.toLocaleString("id-ID", { style: "currency", currency: "IDR" }) }}</h5>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>

const client = useSupabaseClient();
const user = useSupabaseUser(); // Ambil user yang sedang login
const totalPemasukan = ref(0);
const totalPenarikan = ref(0);
const totalBalance = ref(0)
const siswa = ref()

// Fungsi untuk mengambil total pemasukan dan penarikan untuk pengguna yang sedang login
const fetchBalances = async () => {
  try {
    // Pastikan user terdaftar
    if (!user.value) {
      console.warn('User not logged in');
      return;
    }

    const userId = user.value.id; // Ambil ID pengguna yang sedang login

    // Mengambil data pemasukan berdasarkan user ID
    const { data: pemasukanData, error: pemasukanError } = await client
      .from('pemasukan')
      .select('nominal') // Pastikan nama kolom sesuai dengan tabel Anda
      .eq('user_id', userId); // Filter berdasarkan user_id

    // Mengambil data penarikan berdasarkan user ID
    const { data: penarikanData, error: penarikanError } = await client
      .from('penarikan')
      .select('nominal') // Pastikan nama kolom sesuai dengan tabel Anda
      .eq('user_id', userId); // Filter berdasarkan user_id

    // Cek error
    if (pemasukanError) throw new Error(pemasukanError.message);
    if (penarikanError) throw new Error(penarikanError.message);

    // Menjumlahkan total pemasukan
    totalPemasukan.value = pemasukanData ? pemasukanData.reduce((acc, item) => acc + item.nominal, 0) : 0;

    // Menjumlahkan total penarikan
    totalPenarikan.value = penarikanData ? penarikanData.reduce((acc, item) => acc + item.nominal, 0) : 0;

  } catch (error) {
    console.error('Terjadi kesalahan saat mengambil data:', error.message);
  }
};

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

// Memanggil fungsi saat komponen dimuat
onMounted(() => {
  fetchBalances();
  getProfile()
  setTimeout(() => {
    fetchTotalBalance()
  }, 1000);
});
</script>

<style scoped>
.balance-box {
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 20px;
  background-color: #1A9EA7;
  color: white;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}
.balance-box h4 {
  margin: 5px;
}
.balance-box h5 {
  margin: 20px 0 0;
}
</style>

