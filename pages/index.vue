<template>
    <div class="container-fluid">
      <div class="row justify-content-evenly">
        <div class="col-md-3 m-3 d-flex justify-content-end align-items-center siswaa text-center"><nuxt-link to=siswa class="test">Siswa<i class="ms-5 bi bi-person-fill zoom "></i></nuxt-link></div>
        <div class="col-md-3 m-3 d-flex justify-content-end align-items-center tabungann text-center"><nuxt-link to=tabungan class="test">tabungan<i class="ms-4 bi bi-bar-chart-fill zoom"></i></nuxt-link></div>
        <div class="col-md-3 m-3 d-flex justify-content-end align-items-center saldo text-center">Saldo<i class="ms-5 bi bi-pie-chart-fill zoom "></i></div>
      </div>
    </div>
</template>


<style scope>
  .zoom{
    font-size: 100px;
  }
  .siswaa{
    font-size: 30px;
    min-height: 150px;
    background-color: #BCDF5B;
  }
  .tabungann{
    font-size: 30px;
    background-color: #5E99CF;
  }
  .saldo{
    font-size: 30px;
    background-color: #BF4E0E;
  }
</style>