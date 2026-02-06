<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import axios from 'axios'

const router = useRouter()
const name = ref('')
const email = ref('')
const password = ref('')

const register = async () => {
  if (!name.value || !email.value || !password.value) return alert('Nhập đủ thông tin')

  const check = await axios.get(`http://localhost:3000/users?email=${email.value}`)
  if (check.data.length) return alert('Email đã tồn tại')

  await axios.post('http://localhost:3000/users', {
    name: name.value,
    email: email.value,
    password: password.value
  })

  alert('Đăng ký thành công')
  router.push('/login')
}
</script>

<template>
  <div class="container app-section">
    <h3>Đăng ký</h3>
    <input class="form-control mb-2" placeholder="Họ tên" v-model="name" />
    <input class="form-control mb-2" placeholder="Email" v-model="email" />
    <input class="form-control mb-2" type="password" placeholder="Mật khẩu" v-model="password" />
    <button class="btn btn-success w-100" @click="register">Đăng ký</button>
  </div>
</template>
