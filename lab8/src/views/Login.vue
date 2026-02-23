<script>
export default {
  methods: {
    login() {
      this.$router.push({ name: "Dashboard" })
    }
  }
}
</script>

<template>
  <div>
    <h2>Login Page</h2>
    <button @click="login">Login</button>
  </div>
</template>