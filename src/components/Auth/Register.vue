<template>
  <form @submit.prevent="registers">
    <div class="form-group">
      <label for="name">Name</label>
      <input type="text" id="name" class="form-control" v-model="name">
    </div>

    <div class="form-group">
      <label for="email">Email</label>
      <input type="email" id="email" class="form-control" v-model="email">
    </div>

    <div class="form-group">
      <label for="password">Password</label>
      <input type="password" id="password" class="form-control" v-model="password">
    </div>

    <div class="form-group">
      <label for="password_confirmation">Password Confirmation</label>
      <input type="password" id="password_confirmation" class="form-control" v-model="password_confirmation">
    </div>

    <button class="btn btn-success btn-md" type="submit">Register</button>

  </form>
</template>

<script>
import axios from "axios";

require('jquery');
require('bootstrap');

export default {
  data() {
    return {
      name: '',
      email: '',
      password: '',
      password_confirmation: '',
    }
  },
  methods: {
    registers() {
      axios
          .post('http://127.0.0.1:8000/api/users/register/', {
            name: this.name,
            email: this.email,
            password: this.password,
            password_confirmation: this.password_confirmation
          })
          .then((response) => {
            if (response.status === 201) {
              this.$router.push('/');

              window.uid= response.data.data.id

            }
          })
    },
  },
  name: "Register"
}
</script>

<style scoped>

</style>