<template>
  <div class="container-fluid p-5">
      <div class="row mb-5">
        <H1>TABUNGAN</H1>
      </div>
      <form>
        <div class="row mb-3">
          <label for="Kategori" class="kat d-flex mb-3 p-3 col-sm-2 col-form-label">Kategori</label>
          <div class="col-sm-10">
            <select class="form-select" aria-label="Default select example" placeholder="Kategori">
              <option selected>pemasuk/penarik</option>
              <option value="1">pemasukan</option>
              <option value="2">penarikan</option>
            </select>
          </div>
        </div>  
        <div class="row mb-3">
          <label for="id" class="id d-flex mb-3 p-3 col-sm-2 col-form-label">id siswa</label>
          <div class="col-sm-10">
            <input type="id siswa" class="da form-control" id="id siswa">
          </div>
        </div>
        <div class="row mb-3">
          <label for="masukan nominal" class="nom d-flex mb-3 p-3 col-sm-2 col-form-label">Jumlah nominal</label>
          <div class="col-sm-10">
            <input type="nominal" class="no form-control" id="nominal">
          </div>
        </div>
      </form>
    <div class="row justify-content-end p-3">
        <button class="btn btn-secondary">
          kembali
        </button>
        <button class="btn btn-primary ms-5">
          simpan
        </button>
      </div>
    </div>
</template>
<style scope>
  .btn{
    width: 10rem ;
  }
</style>
