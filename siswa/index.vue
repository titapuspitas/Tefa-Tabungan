<template>
  <div>
    <div class="container-fluid jarak pe-3 pt-5 pb-3">
      <div class="row">
        <H1>DATA SISWA</H1>
      </div>
      <div class="row">
        <form class="d-flex mb-3" role="search">
          <input class="form-control  zoom" type="search" placeholder="Search" aria-label="Search">
        </form>
      </div>
      <div class="row">
        <div class="col">
          <table class="table table-bordered">
            <thead>
              <tr>
                <td>No</td>
                <td>nis</td>
                <td>Nama</td>
                <td>Kelas</td>
                <td>Jenis kelamin</td>
                <td>Alamat</td>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>1</td>
                <td>356235</td>
                <td>naula</td>
                <td>xii pplg 1</td>
                <td>p</td>
                <td>tasik</td>
              </tr>
            </tbody>
          </table>
          <div class="row justify-content-end">
            <div class="col-1">
              <button class="btn btn-secondary">
                kembali
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scope>
.jarak{
    background-color: #f4f4f4;
    padding-left: 320px ;
    height: 200vh ;
  }
  .zoom{
    margin-inline-start: 900px;
  }
</style>