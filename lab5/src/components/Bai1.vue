<template>
  <div>
    <p>{{ message }}</p>

    <button @click="updateMessage">
      Thay đổi thông điệp
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const message = ref('Thông điệp ban đầu');

const updateMessage = () => {
  message.value = 'Thông điệp đã được thay đổi!';
};
</script>
