<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'
import axios from 'axios'

const router = useRouter()
const user = JSON.parse(localStorage.getItem('user'))

// form
const title = ref('')
const content = ref('')
const image = ref('')
const editingId = ref(null)

// danh sách bài của user
const myPosts = ref([])

// nếu chưa login thì đá về login
if (!user) router.push('/login')

// load bài của user
const loadMyPosts = async () => {
  const res = await axios.get(
    `http://localhost:3000/posts?userId=${user.id}`
  )
  myPosts.value = res.data
}

onMounted(loadMyPosts)

// thêm hoặc sửa bài
const submitPost = async () => {
  if (!title.value || !content.value) {
    alert('Vui lòng nhập đủ dữ liệu')
    return
  }

  const postData = {
    title: title.value,
    content: content.value,
    image: image.value,
    userId: user.id,
    createdAt: new Date().toLocaleString()
  }

  if (editingId.value) {
    // ✏️ SỬA
    await axios.put(
      `http://localhost:3000/posts/${editingId.value}`,
      postData
    )
    editingId.value = null
  } else {
    // ➕ THÊM
    await axios.post('http://localhost:3000/posts', postData)
  }

  resetForm()
  loadMyPosts()
}

// chọn bài để sửa
const editPost = (post) => {
  title.value = post.title
  content.value = post.content
  image.value = post.image
  editingId.value = post.id
}

// xóa bài
const deletePost = async (id) => {
  if (!confirm('Bạn có chắc muốn xóa bài này?')) return

  await axios.delete(`http://localhost:3000/posts/${id}`)
  loadMyPosts()
}

// reset form
const resetForm = () => {
  title.value = ''
  content.value = ''
  image.value = ''
  editingId.value = null
}
</script>

<template>
  <div class="container app-section">
    <!-- FORM -->
    <h3 class="page-title">
      {{ editingId ? 'Chỉnh sửa bài viết' : 'Đăng bài viết' }}
    </h3>

    <div class="app-form mb-4">
      <input
        class="form-control mb-2"
        placeholder="Tiêu đề"
        v-model="title"
      />
      <textarea
        class="form-control mb-2"
        placeholder="Nội dung"
        v-model="content"
      ></textarea>
      <input
        class="form-control mb-3"
        placeholder="URL hình ảnh"
        v-model="image"
      />

      <button class="btn btn-success me-2" @click="submitPost">
        {{ editingId ? 'Cập nhật' : 'Đăng bài' }}
      </button>

      <button
        v-if="editingId"
        class="btn btn-secondary"
        @click="resetForm"
      >
        Hủy
      </button>
    </div>

    <!-- DANH SÁCH BÀI CỦA TÔI -->
    <h4 class="mb-3">Bài viết của tôi</h4>

    <div
      v-for="post in myPosts"
      :key="post.id"
      class="card app-card mb-3"
    >
      <div class="card-body">
        <h5 class="card-title">{{ post.title }}</h5>
        <p class="card-text">{{ post.content }}</p>
      </div>

      <div class="card-footer d-flex justify-content-end">
        <button
          class="btn btn-sm btn-warning me-2"
          @click="editPost(post)"
        >
          Sửa
        </button>
        <button
          class="btn btn-sm btn-danger"
          @click="deletePost(post.id)"
        >
          Xóa
        </button>
      </div>
    </div>
  </div>
</template>
