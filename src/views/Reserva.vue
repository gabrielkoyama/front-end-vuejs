<template>
  <!-- reserva -->
  <div class="car1d">
    <div class="card-body p-0">
      <h5 class="card-title" style="margin: 10px 10px 0px 10px; padding: 0.65rem; "> </h5>

        <div class="container">
          
        <h3>Reserva atual</h3>
        <p>Sua reserva atual: </p>

        <h1> {{usuario}} </h1>
          <!-- <table class="table table-stripped mt-2 carros">
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
              </tr>
            </tbody>
          </table> -->
        </div>

        <div class="dropdown-divider mt-5"></div>
      
      <div class="container">
        <div class="mt-5">
          
          <h3>Historico de reservas</h3>
          <p>Seu historico de reservas passadas:</p>
          
          <!-- <h1> {{ reserva.carro.nome }} </h1> -->

          <!-- <table class="table table-stripped mt-2 carros">
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
                <td>{{ res.carro.nome}}</td>
                <td>{{ res.carro.modelo}}</td>
                <td>{{ res.data_ini}}</td>
                <td>{{ res.data_fim}}</td>
              </tr>
            </tbody>
          </table> -->
          
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  import { mapState } from 'vuex'

  export default {

    name: 'reserva',
    data() {
      return {
        reserva: [],
      }
    },

    computed: {
      ...mapState([
        'usuario'
      ])
    },

    methods: {
      async atualizar(){

        console.log('/reserva/getById/' + this.usuario.id)
      //   axios.get('/reserva/getById/' + this.usuario.id,
      //     { headers: { Accept: 'application/json' } })
      //   .then(res => {
      //     this.reserva = res.data
      //     console.log(res.data)
      //   })
      //   .catch(error => console.log(error))        
      }
    },

    created() {
      this.atualizar();
    }

  }
</script>