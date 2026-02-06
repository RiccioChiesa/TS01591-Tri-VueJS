<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'
import { useRouter } from 'vue-router'

const router = useRouter()

const name = ref('')
const email = ref('')
const password = ref('')
const avatar = ref('')

let userId = null

onMounted(() => {
  const user = JSON.parse(localStorage.getItem('user'))
  if (!user) return router.push('/login')

  userId = user.id
  name.value = user.name
  email.value = user.email
  avatar.value = user.avatar || ''
})

const updateProfile = async () => {
  if (!name.value || !email.value) {
    alert('Tên và email không được để trống')
    return
  }

  const updatedUser = {
    name: name.value,
    email: email.value,
    avatar: avatar.value
  }

  if (password.value) {
    updatedUser.password = password.value
  }

  const res = await axios.put(
    `http://localhost:3000/users/${userId}`,
    updatedUser
  )

  localStorage.setItem('user', JSON.stringify(res.data))
  alert('Cập nhật thành công')
  password.value = ''
}
</script>

<template>
  <div class="container app-section">
    <div class="profile-card">

      <h3 class="page-title">Thông tin cá nhân</h3>

      <!-- AVATAR -->
      <div class="text-center mb-4">
        <img
          :src="avatar || 'https://baogiaothong.mediacdn.vn/603483875699699712/2024/3/11/428704647-6702272193207187-7873914790208904272-n-656-17101299231521028955862.jpeg'"
          alt="Avatar"
          class="rounded-circle"
          width="120"
          height="120"
        />
      </div>

      <div class="mb-3">
        <label class="form-label">Link ảnh đại diện</label>
        <input
          type="text"
          class="form-control"
          placeholder="https://example.com/avatar.jpg"
          v-model="avatar"
        />
      </div>

      <div class="mb-3">
        <label class="form-label">Họ tên</label>
        <input type="text" class="form-control" v-model="name" />
      </div>

      <div class="mb-3">
        <label class="form-label">Email</label>
        <input type="email" class="form-control" v-model="email" />
      </div>

      <div class="mb-3">
        <label class="form-label">Mật khẩu mới</label>
        <input
          type="password"
          class="form-control"
          placeholder="Nhập mật khẩu mới"
          v-model="password"
        />
      </div>

      <div class="d-flex justify-content-end">
        <button class="btn btn-warning" @click="updateProfile">
          Cập nhật
        </button>
      </div>

    </div>
  </div>
</template>
