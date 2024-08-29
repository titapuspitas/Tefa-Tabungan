<template>
  <div class="tinggi container-fluid">
    <div class="row justify-content-center : justify-">
      <div class="col-3">
        <div class="container shadow p-3" style="background-color: #D9D9D9;">
          <form>
            <div class="mb-3">
              <h2 class="row justify-content-center">Login</h2>
            </div>
            <div class="mb-3">
              <input v-model="email" type="text" class="form-control icon"  placeholder="Username">
            </div>
            <div class="mb-5">
              <input v-model="password" type="password" class="form-control icon-eye" placeholder="password">
            </div>
            <div class="mb-5">
              <button @click="handleLogin" type="button" class="button">masuk</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
definePageMeta({
  layout: 'login',
  middleware: 'auth'
})
const client = useSupabaseClient()
const email = ref("");
const password = ref("");

async function handleLogin() {
  const {error} = await client.auth.signInWithPassword({
    email: email.value,
    password: password.value
  })
  if(!error) RedirectTo('/dashboard')
}
</script>



<style scoped>
.tinggi{
  height: 100vh;
  padding-block: 30vh;
}
.button {
  border: none;
  color: white;
  background: #1A9EA7;
  margin: 4px 5px;
  padding: 5px 10px;
  font-size: 16px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  cursor: pointer;
}
.row{
  padding-block: 25px;
}
.icon {
  background: url("https://img.icons8.com/?size=100&id=98957&format=png&color=000000") no-repeat right;
  background-color: white;
  padding-right: 100px;
  background-size: 35px;
}
.icon-eye {
  background: url("https://img.icons8.com/?size=100&id=oZFC4NAoTr5c&format=png&color=000000") no-repeat right;
  background-color: white;
  padding-right: 100px;
  background-size: 35px;
}

</style>