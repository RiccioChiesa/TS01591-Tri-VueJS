<template>
  <div class="container mt-5" style="max-width: 600px">
    <h3 class="mb-3">Đăng bài viết</h3>

    <div class="mb-3">
      <label class="form-label">Tiêu đề</label>
      <input type="text" class="form-control" placeholder="Nhập tiêu đề bài viết" />
    </div>

    <div class="mb-3">
      <label class="form-label">Nội dung</label>
      <textarea
        class="form-control"
        rows="6"
        placeholder="Nhập nội dung bài viết"
      ></textarea>
    </div>

    <div class="mb-3">
      <label class="form-label">Hình ảnh (URL)</label>
      <input type="text" class="form-control" placeholder="https://..." />
    </div>

    <button class="btn btn-success w-100">Đăng bài</button>
  </div>
</template>
