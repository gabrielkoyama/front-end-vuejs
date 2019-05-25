<template>
  <!-- reserva -->
  <div class="car1d">
    <div class="card-body p-0">
      <h5 class="card-title" style="margin: 10px 10px 0px 10px; padding: 0.65rem; "> </h5>

        <div class="container">
          
        <h3>Reserva atual</h3>
        <p>Sua reserva atual: </p>

          <table class="table table-stripped mt-2 reservas_usr">
            <thead>
              <tr>
                <th>Nome do carro</th>
                <th>Modelo</th>
                <th>Data Inicio</th>
                <th>Data Fim</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="res in reserva_atual" :key="res.id">
                <td>{{ res.carro.nome}}</td>
                <td>{{ res.carro.modelo}}</td>
                <td>{{ res.data_ini}}</td>
                <td>{{ res.data_fim}}</td>
              </tr>
            </tbody>
          </table>

        </div>

        <div class="dropdown-divider mt-5"></div>
      
      <div class="container">
        <div class="mt-5">
          
          <h3>Historico de reservas</h3>
          <p>Seu historico de reservas passadas:</p>
          
          <!-- <span class="p-2"> {{reserva}} </span> -->

          <!-- <h1> {{ reserva.carro.nome }} </h1> -->

          <table class="table table-stripped mt-2 reservas_usr">
            <thead>
              <tr>
                <th>Nome do carro</th>
                <th>Modelo</th>
                <th>Data Inicio</th>
                <th>Data Fim</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="res in reserva_hist" :key="res.id">
                <td>{{ res.carro.nome}}</td>
                <td>{{ res.carro.modelo}}</td>
                <td>{{ res.data_ini}}</td>
                <td>{{ res.data_fim}}</td>
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
  import { mapState } from 'vuex'

  export default {

    name: 'reserva',
    data() {
      return {
        reserva: [],
        reserva_atual: [],
        reserva_hist: []
      }
    },

    computed: {
      ...mapState([
        'usuario'
      ])
    },

    methods: {
      async atualizar(){

        var hj = new Date()

        await axios.get('/reserva/getAll/',
          { headers: { Accept: 'application/json' } })
        .then(res => {
          res.data.filter(( e )=> { return e.usuario.id == this.usuario.id ? this.reserva.push(e) : console.log(''); });
        })
        .catch(error => console.log(error))

        //calculo da reserva atual
        await this.reserva.map((el) => {
          if(new Date(el.data_fim) > hj) this.reserva_atual.push(el)
          else this.reserva_hist.push(el)
        })
        $('.reservas_usr').DataTable();
        $('.reservas_usr_atual').DataTable();
      }
    },
    created() {
      this.atualizar();
    }

  }
</script>