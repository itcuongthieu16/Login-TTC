<template>
  <form @submit.prevent="handleLogin" class="w-[30%] my-auto shadow-2xl p-5">
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
        placeholder="name@flowbite.com"
        required
      />
    </div>
    <div class="mb-6">
      <label
        for="password"
        class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
        >Mật khẩu</label
      >
      <input
        v-model="password"
        type="password"
        id="password"
        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
        required
      />
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
      Đăng nhập
    </button>
  </form>
</template>

<script>
import { toast } from "vue3-toastify";
import "vue3-toastify/dist/index.css";

export default {
  name: "Login",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    async handleLogin() {
      try {
        const users = JSON.parse(localStorage.getItem("userData")) || [];
        const user = this.checkUser(users, this.email, this.password);

        if (user) {
          const loggedInUser = {
            email: user.email,
            isLoggedIn: true,
          };
          localStorage.setItem("loggedInUser", JSON.stringify(loggedInUser));
          this.$emit("loggedin");
          toast.success("Đăng nhập thành công")
          this.$router.push("/");
        } else {
          toast.error("Tài khoản hoặc mật khẩu không chính xác!");
        }
      } catch (error) {
        console.error(error);
        toast.error("Lỗi xảy ra khi đăng nhập!");
      }
    },
    checkUser(users, email, password) {
      return users.find(
        (user) => user.email === email && user.password === password
      );
    },
  },
};
</script>

<style></style>
