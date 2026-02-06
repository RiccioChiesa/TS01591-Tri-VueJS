<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'
import Comment from '../components/Comment.vue'

const posts = ref([])

onMounted(async () => {
  try {
    const res = await axios.get('http://localhost:3000/posts')
    posts.value = res.data
    console.log('POSTS:', posts.value)
  } catch (err) {
    console.error('LỖI LOAD POSTS', err)
  }
})
</script>

<template>
  <div class="container mt-4">
    <h3 class="mb-4">Danh sách bài viết</h3>

    <!-- Không có bài -->
    <div v-if="posts.length === 0" class="alert alert-warning">
      Không có bài viết nào
    </div>

    <!-- Danh sách bài -->
    <div
      v-for="post in posts"
      :key="post.id"
      class="card mb-4"
    >
      <img
        v-if="post.image"
        :src="post.image"
        class="card-img-top"
        style="max-height: 300px; object-fit: cover"
      />

      <div class="card-body">
        <h5 class="card-title">{{ post.title }}</h5>
        <p class="card-text">{{ post.content }}</p>
        <small class="text-muted">📅 {{ post.createdAt }}</small>

        <!-- ===================== -->
        <!-- BÌNH LUẬN CHO BÀI VIẾT -->
        <!-- ===================== -->
        <Comment :postId="post.id" />
      </div>
    </div>
  </div>
</template>
