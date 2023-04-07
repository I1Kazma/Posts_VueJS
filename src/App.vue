/*Разметка*/
<template>
  <navbar></navbar>

  <div class="app">
    <router-view></router-view>
  </div>
</template>

/*Логика*/
<script>
import Navbar from "@/components/UI/Navbar.vue"
export default {
  components: {
    Navbar
  }
}
</script>

/*Стиль*/
<style>
* {
  margin: 0;
  padding: 0;
}
</style>
