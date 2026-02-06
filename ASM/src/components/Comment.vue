<script setup>
import { ref, onMounted, watch } from 'vue'
import axios from 'axios'

const props = defineProps({
  postId: Number
})

const user = JSON.parse(localStorage.getItem('user'))
const comments = ref([])
const newComment = ref('')

// load comment theo post
const loadComments = async () => {
  const res = await axios.get(
    `http://localhost:3000/comments?postId=${props.postId}`
  )
  comments.value = res.data
}

onMounted(loadComments)
watch(() => props.postId, loadComments)

// gửi comment
const submitComment = async () => {
  if (!user) {
    alert('Bạn cần đăng nhập để bình luận')
    return
  }

  if (!newComment.value) return

  await axios.post('http://localhost:3000/comments', {
    postId: props.postId,
    userId: user.id,
    content: newComment.value,
    createdAt: new Date().toLocaleString()
  })

  newComment.value = ''
  loadComments()
}
</script>

<template>
  <div class="mt-3">
    <h6>Bình luận</h6>

    <!-- Danh sách bình luận -->
    <div
      v-for="c in comments"
      :key="c.id"
      class="border rounded p-2 mb-2"
    >
      <strong>User {{ c.userId }}</strong>
      <p class="mb-1">{{ c.content }}</p>
      <small class="text-muted">{{ c.createdAt }}</small>
    </div>

    <!-- Form bình luận -->
    <div v-if="user" class="mt-2">
      <textarea
        class="form-control mb-2"
        rows="2"
        placeholder="Nhập bình luận..."
        v-model="newComment"
      ></textarea>
      <button class="btn btn-sm btn-primary" @click="submitComment">
        Gửi bình luận
      </button>
    </div>

    <div v-else class="text-muted">
      Đăng nhập để bình luận
    </div>
  </div>
</template>
