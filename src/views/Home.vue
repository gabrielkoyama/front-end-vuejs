<template>
  <div>
    <div class="parallax-container">
      <div class="parallax"><img src="assets/img/wpp_car_1.jpg" width="1690px" height="1127px"></div>
      <nav style="background-color: #0000007d;">
        <div class="nav-wrapper">
          <a href="#" class="brand-logo">
            <img src="assets/img/koyata-only.png" width="180px" style="margin-left: 50px !important">
          </a>
          <ul id="nav-mobile" class="right hide-on-med-and-down">
            <li><router-link to="/" class="nav-item">Página Inicial</router-link></li>
            <li><router-link to="/admin" class="nav-item">Admin</router-link></li>
            <li><router-link to="/reserva" class="nav-item">Reserva</router-link></li>
            <li><a v-if="!usuario"><router-link to="/login" class="nav-item">Login</router-link></a></li>
            <li><a v-if="usuario" @click="logout" class="nav-item">Logout</a></li>
          </ul>
        </div>
      </nav>
      <h2 class="header center white-text" style="margin-top: 80px !important">
        Bem-vindo!
      </h2>
      <h5 class="light white-text container">
        <b style="margin-left:80px; font-weight: 300 !important"> Seja </b> bem-vindo a koyota, a maior locadora de carros da américa latina! Agora feita com Java Spring
        Boot e Vue.js!! Sinta-se a vontade para escolher um de nossos carros disponiveis para alugar.
      </h5>
    </div>
    <div class="section white">
      <div class="row container">
        <h3 class="header center">Como funciona <b class="red-text"> ? </b></h3>
        
        <div class="col s12 m3">
          <div class="icon-block">
            <h2 class="center brown-text"><i class="medium material-icons">account_circle</i></h2>
            <h5 class="center">Cadastre-se</h5>
          </div>
        </div>

        <div class="col s12 m3">
          <div class="icon-block">
            <h2 class="center brown-text"><i class="medium material-icons">search</i></h2>
            <h5 class="center">Procure um carro</h5>
          </div>
        </div>

        <div class="col s12 m3">
          <div class="icon-block">
            <h2 class="center brown-text"><i class="medium material-icons">add_shopping_cart</i></h2>
            <h5 class="center">Reserve</h5>
          </div>
        </div>

        <div class="col s12 m3">
          <div class="icon-block">
            <h2 class="center brown-text"><i class="medium material-icons">sentiment_very_satisfied</i></h2>
            <h5 class="center">Use</h5>
          </div>
        </div>
      </div>
    </div>
  <div class="divider"></div>
    <div class="section container">
      <h3 class="header center black-text" style="padding: 40px !important; padding-bottom: 100px !important"> Catálogo de carros </h3>
      <div class="row">
        <div class="col s12 m4" v-for="car in carros" :key="car.id">
          <div class="card hoverable" style="overflow: visible;">
            <div class="card-image waves-effect waves-block waves-light" style="padding: 20px !important">
              <img class="activator" src="assets/img/car_example_1.png" >
            </div>
            <div class="card-content">
              <span class="card-title activator grey-text text-darken-4"> {{car.nome}} <i class="material-icons right">more_vert</i></span>
            </div>
            <div class="card-reveal" style="display: none; transform: translateY(0%);">
              <span class="card-title grey-text text-darken-4">Informações<i class="material-icons right">close</i></span>
              <p class="header">Ano: {{car.ano}} </p>
              <p class="header">Modelo: {{car.modelo}} </p>
              <p class="header">Fabricamte: {{car.fabricante}} </p>
              <p class="header">Cor: {{car.cor}} </p>
              <p class="card-text ini">Periodo Inicio da Reserva: <input type="date" v-model="car.data_ini" ></p>
              <p class="card-text fim">Periodo Fim da Reserva: <input type="date" v-model="car.data_fim" ></p>
              <a class="waves-effect waves-light btn-small" href="#" @click="reservar(car.id, car.data_ini, car.data_fim)">Reservar</a>
            </div>

          </div>
        </div>
      </div>
    </div>
    <a hidden href="" id="error_data" onclick="M.toast({html: 'Por favor, insira o periodo da reserva'})"></a>
    <a hidden href="" id="success" onclick="M.toast({html: 'Carro reservado com sucesso!'})"></a>
  </div>
</template>

<style>
  ::-webkit-scrollbar-track
  {
    -webkit-box-shadow: inset 0 0 6px white;
    border-radius: 5px;
    background-color: rgba(245, 245, 245, 0.431);
  }

  ::-webkit-scrollbar
  {
    width: 5px;
    background-color: #F5F5F5;
  }

  ::-webkit-scrollbar-thumb
  {
    border-radius: 5px;
    -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,.3);
    background-color: #eee;
  }
</style>

<script>

$(document).ready(function(){
  M.AutoInit();
})

$('#myModal').on('shown.bs.modal', function () {
  $('#myInput').trigger('focus')
})

import Datepicker from 'vuejs-datepicker';
import axios from 'axios'
import { mapState } from 'vuex'
import { mapMutations } from 'vuex'

  export default {
    name: 'carros',
     components: {
      Datepicker
    },
    data() {
      return {
        carros: []
      }
    },
    
  computed: {
    ...mapState([
      'usuario'
    ])
  },
  methods: {
    ...mapMutations([
      'logout'
    ]),
    atualizar () {
      axios.get('/carro/getAll', 
          { headers: { Accept: 'application/json' } })
        .then(res => {
          this.carros = res.data
        })
        .catch(error => console.log(error))
    },
    async reservar( id, data_ini, data_fim ) {
      var car;
      var usu;

      console.log(`id: ${id}\ndata_ini: ${data_ini} \ndata_fim: ${data_fim}`)

      if(!data_ini || !data_fim) $('#error_data').click()
      else {
        await axios.get('usuario/getById/' + this.usuario.id)
          .then (res => {
            usu = res.data;
          })
          .catch(error => {
            console.log(error)
          })

        await axios.get('carro/getById/' + id)
          .then (res => {
            car = res.data
          })
          .catch(error => {
            console.log(error)
          })

        var data = {
          usuario: usu,
          carro: car,
          data_ini: data_ini,
          data_fim: data_fim
        }

        axios.post('reserva/save', data )
        .then(res => {
          $('#success').click()
        })
        .catch(error => console.log(error))
      }
    }
  },
  created () {
    this.atualizar()
  }
}
</script>