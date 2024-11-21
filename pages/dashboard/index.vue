<template>
  <div class="container-fluid">
    <div class="row justify-content-center">
      <!-- Siswa (Guru) -->
      <div v-if="userRole == 'guru'" class="col-12 col-md-4 col-lg-3 m-3 d-flex justify-content-center align-items-center siswaa text-center">
        <nuxt-link to="/siswa" class="test">Siswa<i class="ms-3 bi bi-person-fill zoom"></i></nuxt-link>
      </div>

      <!-- Tabungan (Guru) -->
      <div v-if="userRole == 'guru'" class="col-12 col-md-4 col-lg-3 m-3 d-flex justify-content-center align-items-center tabungann text-center">
        <nuxt-link to="/tabungan" class="test">Tabungan<i class="ms-3 bi bi-bar-chart-fill zoom"></i></nuxt-link>
      </div>

      <!-- Profil (Siswa) -->
      <div v-if="userRole == 'siswa'" class="col-12 col-md-4 col-lg-3 m-3 d-flex justify-content-center align-items-center siswaa text-center">
        <nuxt-link to="/siswa" class="test">Profil<i class="ms-3 bi bi-person-fill zoom"></i></nuxt-link>
      </div>

      <!-- Rekapan (Guru) -->
      <div v-if="userRole == 'guru'" class="col-12 col-md-4 col-lg-3 m-3 d-flex justify-content-center align-items-center saldo text-center">
        <nuxt-link to="/rekapan" class="test">Rekapan<i class="ms-3 bi bi-pie-chart-fill zoom"></i></nuxt-link>
      </div>

      <!-- Saldo (Siswa) -->
      <div v-if="userRole == 'siswa'" class="col-12 col-md-4 col-lg-3 m-3 d-flex justify-content-center align-items-center saldo text-center">
        <nuxt-link to="/siswa" class="test">Saldo<i class="ms-3 bi bi-pie-chart-fill zoom"></i></nuxt-link>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
const client = useSupabaseClient();
const user = useSupabaseUser();
const userRole = ref("");

async function getRole() {
  let { data, error } = await client.from("profile").select("role").eq("user_id", user.value.id).single();
  if (error) throw error;
  if (data) userRole.value = data.role;
}

onMounted(() => {
  getRole();
});
</script>

<style scoped>
a {
  text-decoration: none;
}

.test {
  text-align: center;
  color: black;
  font-weight: bold;
}

.zoom {
  font-size: 80px;
}

.siswaa,
.tabungann,
.saldo {
  font-size: 50px;
  min-height: 150px;
  padding: 10px;
  border-radius: 8px;
  box-shadow: 0 8px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s;
  background-color: #f0f0f0;
}

.siswaa {
  background-color: #bcdf5b;
}

.tabungann {
  background-color: #5e99cf;
}

.saldo {
  background-color: #bf4e0e;
}

.siswaa:hover,
.tabungann:hover,
.saldo:hover {
  transform: scale(1.1);
}

/* Media Queries for Responsiveness */
@media (max-width: 768px) {
  .zoom {
    font-size: 50px; /* Smaller icon size on mobile */
  }

  .siswaa,
  .tabungann,
  .saldo {
    font-size: 20px; /* Smaller text on mobile */
  }

  .col-12 {
    margin: 10px 0;
  }
}

@media (min-width: 768px) and (max-width: 992px) {
  .zoom {
    font-size: 60px; /* Adjust icon size for medium screens */
  }

  .siswaa,
  .tabungann,
  .saldo {
    font-size: 25px; /* Medium font size */
  }
}

@media (min-width: 992px) {
  .zoom {
    font-size: 70px; /* Larger icon size for large screens */
  }

  .siswaa,
  .tabungann,
  .saldo {
    font-size: 30px; /* Larger font size for larger screens */
  }
}
</style>
