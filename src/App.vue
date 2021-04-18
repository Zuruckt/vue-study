<template>
  <Navbar></Navbar>
  <div class="content">
    <img alt="Vue logo" src="./assets/logo.png">
<!--    <Contador></Contador>-->
    <CarTable></CarTable>
  </div>

</template>

<script>
require('bootstrap')
import CarTable from "./components/CarTable";
import Navbar from "./components/Navbar";

export default {
  name: 'App',
  components: {
    Navbar,
    CarTable
  }
}


</script>

<style>
@import "https://bootswatch.com/4/lux/bootstrap.min.css";
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.content {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
</style>
