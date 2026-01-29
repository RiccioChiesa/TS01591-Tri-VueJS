<template>
  <div class="container mt-4">
    <h4>Bài 1: Xếp loại học sinh</h4>

    <div class="mb-3">
      <label class="form-label">Nhập điểm trung bình</label>
      <input
        type="number"
        step="0.1"
        class="form-control"
        v-model.number="diemTB"
        placeholder="Nhập điểm..."
      />
    </div>

    <div v-if="diemTB !== null">
      <p v-if="diemTB < 5">Xếp loại: <strong>Yếu</strong></p>
      <p v-else-if="diemTB < 6.5">Xếp loại: <strong>Trung bình</strong></p>
      <p v-else-if="diemTB < 8">Xếp loại: <strong>Khá</strong></p>
      <p v-else-if="diemTB < 9">Xếp loại: <strong>Giỏi</strong></p>
      <p v-else>Xếp loại: <strong>Xuất sắc</strong></p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const diemTB = ref(null)
</script>
