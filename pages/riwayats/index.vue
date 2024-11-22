<template>
  <div class="container-fluid">
    <div class="row justify-content-evenly">
      <div class="col-md-3 m-5 text-center">
        <div class="balance-box">
          <h4>Total Pemasukan</h4>
          <h5>
            {{
              totalPemasukan.toLocaleString("id-ID", {
                style: "currency",
                currency: "IDR",
              })
            }}
          </h5>
        </div>
      </div>
      <div class="col-md-3 m-5 text-center">
        <div class="balance-box">
          <h4>Total Penarikan</h4>
          <h5>
            {{
              totalPenarikan.toLocaleString("id-ID", {
                style: "currency",
                currency: "IDR",
              })
            }}
          </h5>
        </div>
      </div>
      <div class="col-md-3 m-5 text-center">
        <div class="balance-box">
          <h4>Total Saldo</h4>
          <h5>
            {{
              totalBalance.toLocaleString("id-ID", {
                style: "currency",
                currency: "IDR",
              })
            }}
          </h5>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const client = useSupabaseClient();
const user = useSupabaseUser();
const totalPemasukan = ref(0);
const totalPenarikan = ref(0);
const totalBalance = ref(0);
const siswa = ref(null);

const fetchBalances = async () => {
  try {
    // Pastikan user terdaftar
    if (!user.value) {
      console.warn("User not logged in");
      return;
    }

    const userId = user.value.id;

    const { data: pemasukanData, error: pemasukanError } = await client
      .from("pemasukan")
      .select(`
        nominal,
        siswa!inner (
          profile!inner (
            user_id
          )
        )
      `)
      .eq("siswa.profile.user_id", userId)

    const { data: penarikanData, error: penarikanError } = await client
      .from("penarikan")
      .select(`
        nominal,
        siswa!inner (
          profile!inner (
            user_id
          )
        )
      `) 
      .eq("siswa.profile.user_id", userId) 

    // Cek error
    if (pemasukanError) {
      console.error("Error while fetching pemasukan:", pemasukanError.message);
      throw new Error(pemasukanError.message);
    }
    if (penarikanError) {
      console.error("Error while fetching penarikan:", penarikanError.message);
      throw new Error(penarikanError.message);
    }

    totalPemasukan.value = pemasukanData
      ? pemasukanData.reduce((acc, item) => acc + item.nominal, 0)
      : 0;

    totalPenarikan.value = penarikanData
      ? penarikanData.reduce((acc, item) => acc + item.nominal, 0)
      : 0;
  } catch (error) {
    console.error("Terjadi kesalahan saat mengambil data:", error.message);
  }
};

const getProfile = async () => {
  const { data, error } = await client
    .from("profile")
    .select()
    .eq("user_id", user.value.id)
    .single();

  if (data) {
    siswa.value = data;
  }
};

const fetchTotalBalance = async () => {
  try {
    if (!siswa.value) {
      console.warn("Siswa profile not found");
      return;
    }

    const { data, error } = await client
      .from("siswa")
      .select("saldo") 
      .eq("id", siswa.value.id)
      .single();

    if (error) throw new Error(error.message);

    if (data) totalBalance.value = data.saldo; 
  } catch (error) {
    console.error("Terjadi kesalahan saat mengambil saldo:", error.message);
  }
};

onMounted(async () => {
  await fetchBalances(); 
  await getProfile(); 
  await fetchTotalBalance();
});
</script>

<style scoped>
.balance-box {
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 20px;
  background-color: #1a9ea7;
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
