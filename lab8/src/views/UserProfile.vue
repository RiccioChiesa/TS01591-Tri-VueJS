<template>
  <div>
    <h2>User Profile</h2>

    <router-link :to="{ name: 'UserProfileInfo' }">Info</router-link> |
    <router-link :to="{ name: 'UserProfileSettings' }">Settings</router-link>

    <router-view></router-view>
  </div>
</template>