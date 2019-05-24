<template>
  <!-- reserva -->
  <div class="car1d">
    <div class="card-body p-0">
      <h5 class="card-title" style="margin: 10px 10px 0px 10px; padding: 0.65rem; "> </h5>

        <div class="container">
          
        <h3>Reserva atual</h3>
        <p>Sua reserva atual é mostrada abaixo</p>

          <table class="table table-stripped mt-2 carros">
            <thead>
              <tr>
                <th>Nome do carro</th>
                <th>Modelo</th>
                <th>Data Inicio</th>
                <th>Data Fim</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="res in reserva_at" :key="res.id">
                <td>{{}}</td>
                <td>{{}}</td>
                <td>{{}}</td>
                <td>{{}}</td>
                <!-- <td> <a style="cursor: pointer"> <i class="fas fa-edit fa-sm"></i> </a> </td> -->
                <td> <a style="cursor: pointer" :id="car.id" @click="deleteCarById"> <i class="fas fa-trash fa-sm"
                      style="color: red"></i> </a> </td>
              </tr>
            </tbody>
          </table>
        </div>

        <div class="dropdown-divider mt-5"></div>
      
      <div class="container">
        <div class="mt-5">
          
          <h3>Historic  o de reservas</h3>
          <p>Seu historico de reservas e mostrado abaixo</p>

          <table class="table table-stripped mt-2 carros">
            <thead>
              <tr>
                <th>Nome do carro</th>
                <th>Modelo</th>
                <th>Data Inicio</th>
                <th>Data Fim</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="res in reserva" :key="res.id">
                <td>{{}}</td>
                <td>{{}}</td>
                <td>{{}}</td>
                <td>{{}}</td>
                <td> <a style="cursor: pointer" :id="car.id" @click="deleteCarById"> <i class="fas fa-trash fa-sm" style="color: red"></i> </a> </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  import {
    mapState
  } from 'vuex'

  export default {

    name: 'reserva',

    data() {
      return {
        reserva: [],
        reserva_at:[]
      }
    }
  }
</script>