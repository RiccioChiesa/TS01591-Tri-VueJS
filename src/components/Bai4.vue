<template>
  <div class="container mt-4 border p-4">
    <div class="row">
      <!-- FORM -->
      <div class="col-md-4">
        <h5>Thêm học sinh</h5>

        <form @submit.prevent="submitForm">
          <div class="mb-3">
            <label class="form-label">Họ tên:</label>
            <input
              type="text"
              class="form-control"
              v-model="student.name"
            />
          </div>

          <div class="mb-3">
            <label class="form-label">Điểm:</label>
            <input
              type="number"
              class="form-control"
              v-model="student.score"
            />
          </div>

          <div class="mb-3">
            <label class="form-label">Ngày sinh:</label>
            <input
              type="date"
              class="form-control"
              v-model="student.dob"
            />
          </div>

          <button
            type="submit"
            class="btn btn-success"
            v-if="editIndex === -1"
          >
            Thêm
          </button>

          <button
            type="submit"
            class="btn btn-primary"
            v-else
          >
            Cập nhật
          </button>
        </form>
      </div>

      <!-- DANH SÁCH -->
      <div class="col-md-8">
        <h5>Danh sách học sinh</h5>

        <table class="table">
          <thead>
            <tr>
              <th>Họ và tên</th>
              <th>Điểm</th>
              <th>Ngày sinh</th>
              <th></th>
            </tr>
          </thead>

          <tbody>
            <tr v-for="(s, index) in students" :key="index">
              <td>{{ s.name }}</td>
              <td>{{ s.score }}</td>
              <td>{{ s.dob }}</td>
              <td>
                <button
                  class="btn btn-warning btn-sm me-2"
                  @click="editStudent(index)"
                >
                  Sửa
                </button>
                <button
                  class="btn btn-danger btn-sm"
                  @click="deleteStudent(index)"
                >
                  Xóa
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const students = ref([
  {
    name: 'Nguyễn Chí Hùng',
    score: 8,
    dob: '2006-01-01'
  },
  {
    name: 'Phạm Thị Lan',
    score: 9,
    dob: '2006-05-15'
  }
])

const student = ref({
  name: '',
  score: '',
  dob: ''
})

const editIndex = ref(-1)

function submitForm() {
  if (editIndex.value === -1) {
    students.value.push({ ...student.value })
  } else {
    students.value[editIndex.value] = { ...student.value }
    editIndex.value = -1
  }

  student.value = {
    name: '',
    score: '',
    dob: ''
  }
}

function editStudent(index) {
  student.value = { ...students.value[index] }
  editIndex.value = index
}

function deleteStudent(index) {
  students.value.splice(index, 1)
}
</script>
