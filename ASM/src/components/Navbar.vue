<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const isLogin = ref(false)

const checkLogin = () => {
  isLogin.value = !!localStorage.getItem('user')
}

onMounted(() => {
  checkLogin()
})

// logout
const logout = () => {
  localStorage.removeItem('user')
  isLogin.value = false
  router.push('/login')
}
</script>

<template>
  <nav class="navbar navbar-dark bg-dark mb-4">
    <div class="container">
      <span class="navbar-brand">35-NguyenHoangMinhTri</span>

      <div>
        <router-link class="btn btn-outline-light me-2" to="/">Home</router-link>

        <!-- CHƯA LOGIN -->
        <template v-if="!isLogin">
          <router-link class="btn btn-outline-light me-2" to="/login">Login</router-link>
          <router-link class="btn btn-outline-light me-2" to="/register">Register</router-link>
        </template>

        <!-- ĐÃ LOGIN -->
        <template v-else>
          <router-link class="btn btn-outline-light me-2" to="/post/create">
            Đăng bài
          </router-link>
          <router-link class="btn btn-outline-light me-2" to="/profile">
            Profile
          </router-link>
          <button class="btn btn-danger" @click="logout">Logout</button>
        </template>
      </div>
    </div>
  </nav>
</template>
