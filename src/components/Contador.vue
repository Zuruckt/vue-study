<template>
  <div class="form-group">
    <button class="btn btn-primary btn-sm" @click="decrement">-</button>
    <input type="text" v-model="count">
    <button class="btn btn-primary btn-sm" @click="increment">+</button>
    <button class="btn btn-primary btn-sm" @click="multiply">*</button>
  </div>

</template>

<script>

export default {
  data() {
    return {
      count: 0,
    }
  },
  methods: {
    increment() {
      this.count++
    },
    decrement() {
      this.count--
    },
    multiply() {
    }
    // teste() {
    //   fetch('http://127.0.0.1:8000/api/cars/').then(function (response) {
    //     console.log(response.json().then(function (data) { return data}))
    //   })
    // }
  },
  name: "Contador"
}
</script>

<style scoped>

</style>
