<template>
  <div class="container-fluid">
    <div class="row justify-content-evenly">
      <div class="col-md-3 m-3 d-flex justify-content-end align-items-center profil text-center"><nuxt-link to="/identitas" class="test">Profil<i class="ms-5 bi bi-person-fill zoom "></i></nuxt-link></div>
      <div class="col-md-3 m-3 d-flex justify-content-end align-items-center saldo text-center">Saldo<i class="ms-5 bi bi-pie-chart-fill zoom"></i></div>
    </div>
  </div>
</template>

<!-- <script setup>
const user = useSupabaseUser()
console.log(user)
</script> -->

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
  .profil{
    font-size: 30px;
    min-height: 150px;
    background-color: #BCDF5B;
  }
  .saldo{
    font-size: 30px;
    background-color: #BF4E0E;
  }
</style>