<template>
  <Navbar/>
  <div class="container">
    <router-view/>
  </div>
</template>

<script>
import Navbar from "./components/Navbar";
export default {
  components: {
    Navbar
  }
}
</script>

<style scoped>
@import 'https://bootswatch.com/4/lux/bootstrap.min.css'
</style>

