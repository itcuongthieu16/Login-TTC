<template>
  <form @submit.prevent="handleSubmit" class="w-[30%] my-auto shadow-2xl p-5">
    <div class="mb-6">
      <label
        for="usename"
        class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
        >Họ và tên</label
      >
      <input
        v-model="username"
        type="text"
        id="username"
        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
        required
      />
    </div>
    <div class="mb-6">
      <label
        for="email"
        class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
        >Email</label
      >
      <input
        v-model="email"
        type="email"
        id="email"
        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
        placeholder="name@gmail.com"
        required
      />
    </div>
    <div class="mb-6">
      <label
        for="password"
        class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
        >Mật khẩu</label
      >
      <div class="relative">
        <input
          v-model="password"
          :type="showPassword ? 'text' : 'password'"
          id="password"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          required
        />
        <button
          class="absolute top-1/2 right-3 mt-1 transform -translate-y-1/2 focus:outline-none"
          @click="showPassword = !showPassword"
        >
          <!-- <i :class="showPassword ? 'bx bx-low-vision' : 'fas fa-eye'"></i> -->
          <box-icon
            :name="showPassword ? 'show' : 'hide'"
            color="#999"
            size="20px"
          ></box-icon>
        </button>
      </div>
    </div>

    <div class="mb-6">
      <label
        for="confirmPassword"
        class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
        >Nhập lại mật khẩu</label
      >
      <div class="relative">
        <input
          v-model="confirmPassword"
          :type="showPassword ? 'text' : 'password'"
          id="password"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          required
        />
        <button
          class="absolute top-1/2 right-3 mt-1 transform -translate-y-1/2 focus:outline-none"
          @click="showPassword = !showPassword"
        >
          <box-icon
            :name="showPassword ? 'show' : 'hide'"
            color="#999"
            size="20px"
          ></box-icon>
        </button>
      </div>
    </div>
    <div class="flex items-start mb-6">
      <div class="flex items-center h-5">
        <input
          id="remember"
          type="checkbox"
          value=""
          class="w-4 h-4 border border-gray-300 rounded bg-gray-50 focus:ring-3 focus:ring-blue-300 dark:bg-gray-700 dark:border-gray-600 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800"
          required
        />
      </div>
      <label
        for="remember"
        class="ml-2 text-sm font-medium text-gray-900 dark:text-gray-300"
        >Bạn đồng ý với các điều khoản chứ ?</label
      >
    </div>
    <button
      type="submit"
      class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
    >
      Đăng ký
    </button>
  </form>
</template>

<script>
import axios from "axios";
import { toast } from "vue3-toastify";
import "vue3-toastify/dist/index.css";
export default {
  name: "Register",
  data() {
    return {
      username: "",
      email: "",
      password: "",
      confirmPassword: "",
      showPassword: false,
    };
  },

  methods: {
    handleSubmit() {
      if (this.password !== this.confirmPassword) {
        toast.error("Mật khẩu không khớp, vui lòng nhập lại!");
        return;
      }
      if (
        !this.username ||
        !this.email ||
        !this.password ||
        !this.confirmPassword
      ) {
        toast.error("Vui lòng nhập đầy đủ thông tin.");
        return;
      }
      const id = Date.now().toString() + Math.random().toString().substr(2, 5);
      console.log(id);

      const userData = JSON.parse(localStorage.getItem("userData")) || [];
      const newUser = {
        id,
        username: this.username,
        email: this.email,
        password: this.password,
      };
      userData.push(newUser);
      toast.success("Tạo tài khoản thành công");
      this.$router.push("/login");
      localStorage.setItem("userData", JSON.stringify(userData));
    },
  },
};
</script>

<style></style>
