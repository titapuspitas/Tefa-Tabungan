<template>
    <nav class="navbar fixed">
      <div class="container-fluid">
        <span class="navbar-brand mb-0 h1">Selamat Datang Di Tabungan {{ judul }}</span>
      </div>
    </nav>
</template>

<script setup>
defineProps({
  judul: String
})
</script>

<style scoped>
.navbar{
  background: #1A9EA7;
  height: 15vh;
}
.navbar-brand{
  color: white;
  font-size: 40px;
}
</style>

