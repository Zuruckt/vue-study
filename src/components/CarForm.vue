<template>
  <form action="">
    <div class="form-group">
      <input v-model="model" type="text">
    </div>

    <select v-model="brand_id" >
      <option v-bind:value="brand.id" :key="brand" v-for="brand in brands">{{brand.name}}</option>
    </select>
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
  mounted() {
    axios
        .get('http://127.0.0.1:8000/api/brands/')
        .then(response => (this.brands = response.data.data))
  },
  name: "CarForm"
}
</script>

<style scoped>

</style>