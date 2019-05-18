<template>

<div class="container mt-5">
  <fieldset>
    <legend class=''><strong>Lista de Carros Disponiveis</strong></legend>
    <p>
      Aqui voce podera consultar os carros que ja estão reservados e os carros que estao disponveis


    </p>
  <table class="table">
    <thead class="thead-dark">
      <tr>
        <th scope="col">ID</th>
        <th scope="col">Nome</th>
        <th scope="col">Km</th>
        <th scope="col">Categoria</th>
        <th scope="col">Modelo</th>
        <th scope="col">Ano</th>
        <th scope="col">Fabricante</th>
        <th scope="col">Cor</th>
        <th scope="col">Disponivel</th>
        <th scope="col">Status</th>

      </tr>
    </thead>
    <tbody>
       <tr>
        <th scope="col"></th>
        <th scope="col"></th>
        <th scope="col"></th>
        <th scope="col"></th>
        <th scope="col"></th>
        <th scope="col"></th>
        <th scope="col"></th>
        <th scope="col"></th>
        <th scope="col"></th>
      </tr>
    </tbody>
  </table>
    
  <button type="button" class="btn btn-success">Meus carros reservados</button>
  </fieldset>
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
        carros: []
      }
    }
  }
</script>