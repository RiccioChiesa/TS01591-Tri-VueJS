    <template>
    <div class="col-sm-8" style="margin-top: 40px">
        <h3>Thông tin cá nhân</h3>

        <form>
        <div class="mb-3">
            <label>Họ và Tên:</label>
            <input
            type="text"
            class="form-control"
            v-model="userInfo.name"
            placeholder="Nhập họ và tên"
            />
        </div>

        <div class="mb-3">
            <label>Tuổi:</label>
            <input
            type="number"
            class="form-control"
            v-model="userInfo.age"
            placeholder="Nhập tuổi"
            />
        </div>

        <div class="mb-3">
            <label>Email:</label>
            <input
            type="email"
            class="form-control"
            v-model="userInfo.email"
            placeholder="Nhập email"
            />
        </div>
        </form>

        <!-- Hiển thị thông tin ngay sau khi nhập -->
        <div class="mt-4 p-3 bg-dark text-white rounded">
        <h4>Thông tin đã nhập:</h4>
        <p><strong>Họ và Tên:</strong> {{ userInfo.name }}</p>
        <p><strong>Tuổi:</strong> {{ userInfo.age }}</p>
        <p><strong>Email:</strong> {{ userInfo.email }}</p>
        </div>
    </div>
    </template>

    <script setup>
    import { reactive } from 'vue';

    const userInfo = reactive({
    name: '',
    age: null,
    email: ''
    });
    </script>
