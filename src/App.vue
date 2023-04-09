<template>
  <div id="app">
    <Nav />

    <div class="w-full h-[100vh] flex justify-center">
      <router-view />
    </div>
  </div>
</template>

<script>
import Nav from "./components/Nav.vue";

export default {
  name: "App",
  components: {
    Nav,
  },
};
</script>

<style></style>
