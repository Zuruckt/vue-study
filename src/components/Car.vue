<template>
  <form @submit.prevent="addCar" class="w-100">
    <div class="form-group">
      <label for="model">Modelo</label>
      <input class="form-control" v-model="car.model" type="text" id="model">
    </div>

    <div class="form-group">
      <label for="brand">Marca</label>
      <select class="form-control" v-model="car.brand_id" id="brand">
        <option v-bind:value="brand.id" :key="brand" v-for="brand in brands">{{brand.name}}</option>
      </select>
    </div>

    <div class="form-group">
      <label for="year">Ano</label>
      <input class="form-control" v-model="car.year" type="text" id="year">
    </div>
//
    <button class="btn btn-success btn-md">Criar</button>
  </form>

  <div class="w-100 mt-1">
    <h3>Lista de Carros</h3>
    <table class="table">
      <thead>
        <td>Modelo</td>
        <td>Marca</td>
        <td>Ano</td>
        <td>Editar</td>
        <td>Deletar</td>
      </thead>
      <tbody v-bind:key="car" v-for="car in cars">
        <td>{{ car.model }}</td>
        <td>{{ car.brand_name }}</td>
        <td>{{ car.year }}</td>
        <td><button type="button" class="btn btn-warning btn-md" @click="showEditModal(car.id)" data-toggle="modal" data-target="#editCarModal">Editar</button></td>
        <td><button class="btn btn-danger btn-md" @click="deleteCar(car.id)">Deletar</button></td>
      </tbody>
    </table>
  </div>


  <div class="modal fade" id="editCarModal" tabindex="-1" role="dialog" aria-labelledby="editCarModal" aria-hidden="true">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">Editar Carro</h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
            <div class="form-group">
              <label for="edit-model">Modelo</label>
              <input class="form-control" v-model="editCar.model" type="text" id="edit-model">
            </div>

            <div class="form-group">
              <label for="edit-brand">Marca</label>
              <select class="form-control" v-model="editCar.brand_id" id="edit-brand">
                <option v-bind:value="brand.id" :key="brand" v-for="brand in brands">{{brand.name}}</option>
              </select>
            </div>

            <div class="form-group">
              <label for="edit-year">Ano</label>
              <input class="form-control" v-model="editCar.year" type="text" id="edit-year">
            </div>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
          <button type="button" @click="updateCar" data-dismiss="modal" class="btn btn-primary">Save changes</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
require('jquery');
require('bootstrap');

export default {
  data() {
    return {
      car: {
        id: null,
        model: null,
        year: null,
        brand_id: null,
      },
      brands: [],
      cars: [],
      editCar: [],
      selectedBrand: null,
    }
  },
  methods: {
    addCar() {
      axios
          .post('http://127.0.0.1:8000/api/cars/', {
            model: this.car.model,
            year: this.car.year,
            brand_id: this.car.brand_id
          })
          .then((response) => {
            this.cars.push(response.data.data)
          })
    },
    showEditModal(id) {
      this.editCar = JSON.parse(JSON.stringify(this.cars.find(element => element.id === id)));
      console.log(this.editCar, this.cars)
      this.selectedBrand = this.editCar.brand_id;
    },
    updateCar() {
      axios
          .put('http://127.0.0.1:8000/api/cars/' + this.editCar.id, {
            model: this.editCar.model,
            year: this.editCar.year,
            brand_id: this.editCar.brand_id
          })
          .then((response) => {
            this.cars[this.cars.findIndex(element => element.id === this.editCar.id)] = response.data.data;
          })
          .catch((error) => console.log(error));
    },
    deleteCar(id) {
      axios
          .delete('http://127.0.0.1:8000/api/cars/' + id)
          .then(() => {
            this.cars.splice(this.cars.findIndex(element => element.id === id), 1);
          })
          .catch((error) => console.log(error));
    },
  },
  mounted() {
    axios
        .get('http://127.0.0.1:8000/api/cars/')
        .then(response => (this.cars = response.data.data))
        .catch((error) => console.log(error));
    axios
        .get('http://127.0.0.1:8000/api/brands/')
        .then(response => (this.brands = response.data.data))
        .catch((error) => console.log(error))
  },
  name: "Car"
}
</script>

<style scoped>

</style>