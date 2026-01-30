<template>
  <div class="container mt-5">
    <h3 class="text-center">Danh sách bài viết</h3>

    <div class="row mt-4">
      <div class="col-sm-4" v-for="(post, index) in posts" :key="index">
        <div class="card">
          <img :src="post.image" class="card-img-top" />
          <div class="card-body">
            <h5 class="card-title">{{ post.title }}</h5>
            <p class="card-text">{{ post.content }}</p>
                   <button class="btn btn-info">Xem chi tiết</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import img1 from '../assets/images/img1.jpg'
import img2 from '../assets/images/img2.jpg'
import img3 from '../assets/images/img3.jpg'

const posts = [
  {
    title: '8 loại rau củ quả giàu canxi',
    content: 'Canxi rất cần thiết cho xương và răng...',
    image: img1
  },
  {
    title: 'Các loại gia vị tốt cho sức khỏe',
    content: 'Một số loại gia vị giúp tăng sức đề kháng...',
    image: img2
  },
  {
    title: '9 loại đậu bổ dưỡng',
    content: 'Đậu lăng và các loại đậu rất giàu protein...',
    image: img3
  }
]
</script>
