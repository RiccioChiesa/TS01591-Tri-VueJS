<script setup>
import { ref } from 'vue'

const emit = defineEmits(['add-post'])

const title = ref('')
const author = ref('')
const content = ref('')

const submitPost = () => {
  if (!title.value || !author.value || !content.value) return

  emit('add-post', {
    title: title.value,
    author: author.value,
    content: content.value,
    // dùng cho style binding
    color: title.value.length > 15 ? 'red' : 'green'
  })

  // reset form
  title.value = ''
  author.value = ''
  content.value = ''
}

</script>
<template>
  <div class="box">
    <h3>Tạo bài viết</h3>

    <input v-model="title" placeholder="Tiêu đề" />
    <input v-model="author" placeholder="Tác giả" />
    <textarea v-model="content" placeholder="Nội dung"></textarea>

    <button @click="submitPost">Đăng bài</button>
  </div>
</template>

<style scoped>
input, textarea {
  width: 100%;
  margin-bottom: 8px;
  padding: 6px;
}
button {
  padding: 6px 12px;
}
</style>
