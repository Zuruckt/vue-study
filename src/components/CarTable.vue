<template>
  <div>
    <table class="table">
      <thead>
        <td>Modelo</td>
        <td>Marca</td>
        <td>Ano</td>
      </thead>

      <tbody v-bind:key="car" v-for="car in cars">
        <td>{{ car.model }}</td>
        <td>{{ car.brand_name }}</td>
        <td>{{ car.year }}</td>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      cars: null
    }
  },
  mounted() {
    axios
        .get('http://127.0.0.1:8000/api/cars/')
        .then(response => (this.cars = response.data.data))
  },
  name: "CarTable"
}
</script>

<style scoped>

</style>