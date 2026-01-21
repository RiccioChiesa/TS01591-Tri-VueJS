<script setup>
import { ref, computed } from 'vue'

const yearOfBirth = ref('')
const currentYear = new Date().getFullYear()

const age = computed(() => {
  if (!yearOfBirth.value) return null
  const year = parseInt(yearOfBirth.value)
  if (isNaN(year) || year < 1900 || year > currentYear) return null
  return currentYear - year
})

const ageCategory = computed(() => {
  if (age.value === null) return ''
  
  if (age.value < 12) {
    return 'Trẻ em'
  } else if (age.value < 18) {
    return 'Thiếu niên'
  } else if (age.value < 40) {
    return 'Thanh niên'
  } else if (age.value < 60) {
    return 'Trung niên'
  } else {
    return 'Lớn tuổi'
  }
})

const isValidInput = computed(() => {
  return age.value !== null
})
</script>

<template>
  <div class="age-calculator">
    <h2>Tính Tuổi</h2>
    
    <div class="input-group">
      <label for="yearInput">Nhập năm sinh:</label>
      <input 
        id="yearInput"
        v-model="yearOfBirth"
        type="number"
        :min="1900"
        :max="currentYear"
      />
    </div>

    <div v-if="isValidInput" class="results">
      <div class="result-item">
        <strong>Năm sinh:</strong> {{ yearOfBirth }}
      </div>
      <div class="result-item">
        <strong>Tuổi:</strong> {{ age }} tuổi
      </div>
      <div class="result-item category">
        <strong>Phân loại:</strong> <span class="category-tag">{{ ageCategory }}</span>
      </div>
    </div>

    <div v-else-if="yearOfBirth" class="error">
      Vui lòng nhập năm sinh hợp lệ (1900 - {{ currentYear }})
    </div>
  </div>
</template>

<style scoped>
.age-calculator {
  max-width: 400px;
  margin: 2rem auto;
  padding: 1.5rem;
}

h2 {
  text-align: center;
  margin-bottom: 1.5rem;
}

.input-group {
  margin-bottom: 1.5rem;
}

label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: bold;
}

input {
  width: 100%;
  padding: 0.5rem;
  font-size: 1rem;
  border: 1px solid #ccc;
  box-sizing: border-box;
}

.results {
  margin-top: 1.5rem;
  padding: 1rem;
  border: 1px solid #ddd;
}

.result-item {
  margin-bottom: 0.75rem;
}

.result-item strong {
  margin-right: 0.5rem;
}

.category-tag {
  padding: 0.25rem 0.5rem;
  margin-left: 0.5rem;
}

.error {
  padding: 0.75rem;
  margin-top: 1rem;
  background-color: #ffebee;
}
</style>