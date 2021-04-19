<template>
  <CarForm @carAdded="carAddedEvent"/>
  <div class="w-100 mt-1">
    <h3>Lista de Carros</h3>
    <table class="table">
      <thead>
      <td>Modelo</td>
      <td>Marca</td>
      <td>Ano</td>
      <td>Deletar</td>
      </thead>

      <tbody v-bind:key="car" v-for="car in cars">
      <td>{{ car.model }}</td>
      <td>{{ car.brand_name }}</td>
      <td>{{ car.year }}</td>
      <td><button class="btn btn-danger btn-md" @click="deleteCar(car.id)">Deletar</button></td>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'
// @ is an alias to /src
import CarForm from '@/components/Car/CarForm.vue'

export default {
  data() {
    return {
      cars: null
    }
  },
  props: {
    newCar: Object
  },
  methods: {
    deleteCar(id) {
      axios.delete('http://127.0.0.1:8000/api/cars/' + id)
          .then(() => {
            this.cars.splice(this.cars.findIndex(element => element.id === id), 1);
          })
    },
    carAddedEvent(data) {
      this.cars.push(data)
    }
  },
  mounted() {
    axios
        .get('http://127.0.0.1:8000/api/cars/')
        .then(response => (this.cars = response.data.data))
  },
  components: {
    CarForm
  },
  name: "CarTable"
}
</script>

<style scoped>

</style>