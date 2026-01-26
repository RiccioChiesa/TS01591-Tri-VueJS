<script setup>
import { ref } from 'vue'
import CreatePost from './CreatePost.vue'
import PostList from './PostList.vue'

const posts = ref([])

const addPost = (post) => {
  posts.value.push(post)
}
</script>

<template>
  <div class="box">
    <h2>Bài 4</h2>

    <CreatePost @add-post="addPost" />
    <PostList :posts="posts" />
  </div>
</template>
