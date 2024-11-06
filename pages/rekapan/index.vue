<template>
  <div class="container-fluid">
    <div class="row">
      <h2 class="text-center my-4">REKAPAN DATA PERBULAN</h2>
      <div class="col-lg-12">
        <nuxt-link to="/dashboard">
          <button type="button" class="btn btn-lg rounded-5 px-5 bg-secondary text-white mb-3">
            KEMBALI
          </button>
        </nuxt-link>

        <div class="warna my-3" style="border-radius: 5px;">
          <h5 style="color: white; text-align: center;">
            JUMLAH TABUNGAN SAAT INI: {{ jumlah_tabungan.toLocaleString("id-ID", { style: "currency", currency: "IDR" }) }}
          </h5>
        </div>

        <div class="table-responsive">
          <table class="table table-striped">
            <thead>
              <tr>
                <th>No</th>
                <th>Bulan</th>
                <th>Tahun</th>
                <th>Pemasukan</th>
                <th>Penarikan</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(rekapan, i) in rekapData" :key="i">
                <td>{{ i + 1 }}</td>
                <td>{{ rekapan.bulan }}</td>
                <td>{{ rekapan.tahun }}</td>
                <td>{{ rekapan.pemasukan.toLocaleString("id-ID", { style: "currency", currency: "IDR" }) }}</td>
                <td>{{ rekapan.penarikan.toLocaleString("id-ID", { style: "currency", currency: "IDR" }) }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient();
const rekapData = ref([]);

// Menghitung total tabungan
const jumlah_tabungan = computed(() => {
  return rekapData.value.reduce((total, rekapan) => {
    return total + rekapan.pemasukan - rekapan.penarikan;
  }, 0);
});

// Mengambil data dari Supabase
const fetchRekapData = async () => {
  try {
    // Ambil data pemasukan dan penarikan
    const [pemasukanData, penarikanData] = await Promise.all([
      supabase.from("pemasukan").select('tanggal, bulan (nama), jumlah'),
      supabase.from("penarikan").select('tanggal, bulan (nama), jumlah')
    ]);

    if (pemasukanData.error || penarikanData.error) {
      throw new Error("Error fetching data");
    }

    const monthlyData = {};

    // Memproses Pemasukan
    pemasukanData.data.forEach(transaction => {
      const date = new Date(transaction.tanggal);
      const year = date.getFullYear();
      const month = transaction.bulan.nama;
      const key = `${year}-${month}`;

      if (!monthlyData[key]) {
        monthlyData[key] = {
          bulan: month,
          tahun: year,
          pemasukan: 0,
          penarikan: 0,
        };
      }
      monthlyData[key].pemasukan += transaction.jumlah;
    });

    // Memproses Penarikan
    penarikanData.data.forEach(transaction => {
      const date = new Date(transaction.tanggal);
      const year = date.getFullYear();
      const month = transaction.bulan.nama;
      const key = `${year}-${month}`;

      if (!monthlyData[key]) {
        monthlyData[key] = {
          bulan: month,
          tahun: year,
          pemasukan: 0,
          penarikan: 0,
        };
      }
      monthlyData[key].penarikan += transaction.jumlah;
    });

    // Mengurutkan data berdasarkan bulan dan tahun
    rekapData.value = Object.values(monthlyData).sort((a, b) => {
      const dateA = new Date(`${a.tahun}-${getMonthNumber(a.bulan)}-01`);
      const dateB = new Date(`${b.tahun}-${getMonthNumber(b.bulan)}-01`);
      return dateB - dateA; // Urutkan dari terbaru
    });
  } catch (error) {
    console.error("Terjadi kesalahan saat mengambil data rekap:", error.message);
  }
};

// Mendapatkan nomor bulan dari nama
const getMonthNumber = (monthName) => {
  const months = [
    "Januari", "Februari", "Maret", "April", "Mei", "Juni",
    "Juli", "Agustus", "September", "Oktober", "November", "Desember"
  ];
  return months.indexOf(monthName) + 1;
};

// Mengambil data saat komponen dimuat
onMounted(() => {
  fetchRekapData();
});
</script>

<style scoped>
.table-responsive {
  overflow-x: auto;
}
h2 {
  color: black;
}
.table-striped th, .table-striped td {
  white-space: nowrap;
}
@media (max-width: 576px) {
  .table-responsive {
    font-size: 12px;
  }
  .btn {
    padding: 12px;
    font-size: 14px;
  }
}
@media (min-width: 992px) {
  .float-lg-end {
    float: right;
  }
}
.warna{
  background: #1A9EA7;
}
</style>
