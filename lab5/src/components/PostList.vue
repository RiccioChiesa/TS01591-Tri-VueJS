<script setup>
defineProps({
  posts: Array
})
</script>

<template>
  <div v-for="(post, index) in posts" :key="index" class="post" :class="{ highlight: post.title.length > 15 }">

  <h4 class="title">{{ post.title }}</h4>
  <p class="author">{{ post.author }}</p>
  <p class="content">{{ post.content }}</p>
</div>

</template>

<style scoped>
.post {
  border: 1px solid #ccc;
  padding: 14px;
  margin-bottom: 15px;
  background: #222;
}
.title {
  color: #208048;
  font-weight: 600;
  margin-bottom: 6px;
}
.author {
  color: #ff4d4f;
  font-weight: 600;
  font-size: 15px;
  margin-bottom: 8px;
  text-shadow: 0 1px 2px rgba(0,0,0,0.5);
}
.content {
  color: #ffffff;
  line-height: 1.5;
}
.highlight {
  border: 2px solid orange;
}

</style>
