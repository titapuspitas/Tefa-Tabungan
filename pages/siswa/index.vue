<template>
    <div class="container-fluid pe-3 pt-5 pb-3">
      <div class="row text-center p-5">
        <H1>DATA SISWA</H1>
      </div>
      <div class="row justify-content-end">
        <div class="col-5">
          <form class="d-flex mb-3" role="search">
            <input class="form-control" type="search" placeholder="Search" aria-label="Search">
          </form>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <table class="table table-bordered">
            <thead>
              <tr>
                <td>No</td>
                <td>nis</td>
                <td>Nama</td>
                <td>Jenis kelamin</td>
                <td>Alamat</td>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>1</td>
                <td>356235</td>
                <td>naula</td>
                <td>p</td>
                <td>tasik</td>
              </tr>
            </tbody>
          </table>
          <nuxt-link to="/dashboard">
            <div class="position-absolute top-70 end-0 p-5">
              <div class="col-1">
                <button class="btn btn-secondary">
                  kembali
                </button>
              </div>
            </div>
          </nuxt-link>
        </div>
      </div>
    </div>

</template>

<style scope>

</style>