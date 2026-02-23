<script>
export default {
  computed: {
    blog() {
      const blogs = {
        1: {
          title: "Blog 1 Title",
          content: "Messi được minh oan vụ đối chất trọng tài MLS."
        },
        2: {
          title: "Blog 2 Title",
          content: "Trung Quốc hối thúc Mỹ hủy bỏ các khoản thuế đối ứng đơn phương"
        }
      };

      return blogs[this.$route.params.id];
    }
  }
};
</script>

<template>
  <div v-if="blog">
    <h2>{{ blog.title }}</h2>
    <p>{{ blog.content }}</p>
  </div>

  <div v-else>
    <h2>Blog not found</h2>
  </div>
</template>