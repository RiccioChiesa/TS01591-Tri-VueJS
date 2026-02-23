<template>
  <div>
    <h1>Welcome to MyBlog</h1>

    <router-link to="/">Home</router-link> |
    <router-link :to="{ name: 'BlogList' }">Blog</router-link> |
    <router-link :to="{ name: 'UserProfile' }">Profile</router-link> |
    <router-link :to="{ name: 'Dashboard' }">Dashboard</router-link> |
    <router-link :to="{ name: 'Login' }">Login</router-link>
  </div>
</template>