<template>
  <form @submit.prevent="addCar" class="w-100">
    <div class="form-group">
      <label for="model">Modelo</label>
      <input class="form-control" v-model="model" type="text" id="model">
    </div>

    <div class="form-group">
      <label for="brand">Marca</label>
      <select class="form-control" v-model="brand_id" id="brand">
        <option v-bind:value="brand.id" :key="brand" v-for="brand in brands">{{brand.name}}</option>
      </select>
    </div>

    <div class="form-group">
      <label for="year">Ano</label>
      <input class="form-control" v-model="year" type="text" id="year">
    </div>

    <button class="btn btn-success btn-md">Criar</button>
  </form>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      model: '',
      year: '',
      brand_id: null,
      brands: null
    }
  },
  methods: {
    addCar() {
      axios
          .post('http://127.0.0.1:8000/api/cars/', {
            model: this.model,
            year: this.year,
            brand_id: this.brand_id
          })
          .then((response) => {
            this.$emit('carAdded', response.data.data)
          })
    },
  },
  mounted() {
    axios
        .get('http://127.0.0.1:8000/api/brands/')
        .then(response => (this.brands = response.data.data))
        .catch((error) => console.log(error))
  },
  name: "CarForm"
}
</script>

<style scoped>

</style>