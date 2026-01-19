<template>
  <div class="container mt-4">
    <h3>Danh sách bài viết</h3>

    <div class="card mb-3" v-for="i in 3" :key="i">
      <div class="card-body">
        <h5 class="card-title">Bài viết {{ i }}</h5>
        <p class="card-text">Nội dung mô tả bài viết...</p>
      </div>
    </div>
  </div>
</template>
