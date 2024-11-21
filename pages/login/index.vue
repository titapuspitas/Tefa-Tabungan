<template>
  <div class="tinggi container-fluid">
    <div class="row justify-content-center">
      <div class="col-3">
        <div class="container shadow p-3" style="background-color: #D9D9D9;">
          <form>
            <div class="mb-3">
              <h2 class="row justify-content-center">Login</h2>
            </div>

            <!-- Email Field -->
            <div class="mb-3 position-relative">
              <input 
                v-model="email" 
                type="text" 
                class="form-control icon"  
                placeholder="Username">
              <i class="bi bi-person-fill position-absolute top-50 end-0 translate-middle-y me-3"></i>
            </div>

            <!-- Password Field -->
            <div class="mb-5 position-relative">
              <input 
                v-model="password" 
                :type="isPasswordVisible ? 'text' : 'password'" 
                class="form-control icon-gembok" 
                placeholder="Password">
              <i 
                @click="togglePasswordVisibility"
                :class="isPasswordVisible ? 'bi bi-eye-fill' : 'bi bi-eye-slash-fill'" 
                class="position-absolute top-50 end-0 translate-middle-y me-3"
                style="cursor: pointer;"></i>
            </div>

            <!-- Error Message -->
            <div v-if="errorMessage" class="mb-3 text-danger text-center">
              {{ errorMessage }}
            </div>

            <!-- Login Button -->
            <div class="mb-5">
              <button @click="handleLogin" type="button" class="button">Masuk</button>
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
})

const client = useSupabaseClient()
const email = ref("")
const password = ref("")
const isPasswordVisible = ref(false)
const errorMessage = ref("")  // Store error message

// Function to handle login
async function handleLogin() {
  const { data, error } = await client.auth.signInWithPassword({
    email: email.value,
    password: password.value,
  })

  if (error) {
    // Check the error type and assign the appropriate error message
    if (error.message.includes("invalid email")) {
      errorMessage.value = "Email yang anda masukkan salah"
    } else if (error.message.includes("incorrect password")) {
      errorMessage.value = "Password yang anda masukkan salah"
    } else {
      errorMessage.value = "Periksa lebih teliti !!!"
    }
    
    // Clear error message after 3 seconds
    setTimeout(() => {
      errorMessage.value = ""
    }, 1000)
    return
  }

  if (data) {
    getProfileRole(data.user.id)
  }
}

// Function to get user role after login
async function getProfileRole(id) {
  const { data, error } = await client
    .from('profile')
    .select('role')
    .eq('user_id', id)
    .single()
  if (data) {
    if (data.role == 'siswa') navigateTo('/murid')
    else navigateTo('/dashboard')
  }
}

// Toggle password visibility
function togglePasswordVisibility() {
  isPasswordVisible.value = !isPasswordVisible.value
}
</script>

<style scoped>
@media (max-width: 768px) {
    body {
        font-size: 14px;
    }
    .menu {
        display: none;
    }
}
@media (min-width: 769px) {
    body {
        font-size: 18px;
    }
    .menu {
        display: block;
    }
}

.tinggi {
  height: 100vh;
  padding-block: 20vh;
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
.row {
  padding-block: 25px;
}
.icon {
  background-color: white;
  padding-left: 40px;
  padding-right: 40px;
  background-size: 25px;
}
.icon-gembok {
  background-color: white;
  padding-left: 40px;
  padding-right: 40px;
  background-size: 25px;
}
.position-relative {
  position: relative;
}
</style>
