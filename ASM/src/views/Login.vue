<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import axios from 'axios'

const router = useRouter()
const email = ref('')
const password = ref('')

const login = async () => {
  const res = await axios.get(
    `http://localhost:3000/users?email=${email.value}&password=${password.value}`
  )
  if (!res.data.length) return alert('Sai tài khoản')

  localStorage.setItem('user', JSON.stringify(res.data[0]))
  router.push('/')
}
</script>

<template>
  <div class="container app-section">
    <h3>Đăng nhập</h3>
    <input class="form-control mb-2" placeholder="Email" v-model="email" />
    <input class="form-control mb-2" type="password" placeholder="Mật khẩu" v-model="password" />
    <button class="btn btn-primary w-100" @click="login">Đăng nhập</button>
  </div>
</template>
