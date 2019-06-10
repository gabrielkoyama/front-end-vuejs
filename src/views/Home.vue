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
        <h3 class="header center">Como funciona <b class="brown-text"> ? </b></h3>
        
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
      <h3 class="header center black-text" style="padding: 40px !important; padding-bottom: 100px !important"> Catálogo de carros <i class="medium material-icons brown-text">directions_car</i></h3>
<!-- 
      <div class="col-md-4 mt-5">
        <div class="card" style="width: 18rem;">
          <div class="card-body">
            <h5 class="card-title"> car.nome </h5>
            <h6 class="card-subtitle mb-2 text-muted"> car.categoria </h6>
            <hr>
            <span class="card-text"> <b>Modelo: </b>  car.modelo </span> <br>
            <span class="card-text">  <b>Ano: </b> car.ano </span><br>
            <span class="card-text">  <b>Fabricante: </b> car.fabricante </span><br>
            <span class="card-text">  <b>Cor: </b> car.cor </span><br>
            <span class="card-text ini">  <b>Inicio: </b> <input type="date" class="form-control"> </span>
            <span class="card-text fim">  <b>Fim: </b> <input type="date" class="form-control"> </span>
            <hr>
            <a class="card-link" style="cursor: pointer" :id="car.id" @click="reservar" >Reservar</a>
          </div>
        </div>
      </div> -->

      <!-- <div class="card-panel hoverable"> 
        <div class="row">
            <div class="card-content">
              <p>I am a very simple card. I am good at containing small bits of information. I am convenient because I require little markup to use effectively.</p>
            </div>
        </div>
      </div> -->
      <div class="row">
        <div class="col s12 m4">
          <div class="card hoverable" style="overflow: visible;">
            <div class="card-image waves-effect waves-block waves-light" style="padding: 20px !important">
              <img class="activator" src="assets/img/car_example_1.png">
            </div>
            <div class="card-content">
              <span class="card-title activator grey-text text-darken-4">Nome do carro<i class="material-icons right">more_vert</i></span>
            </div>
            <div class="card-reveal" style="display: none; transform: translateY(0%);">
              <span class="card-title grey-text text-darken-4">Informações<i class="material-icons right">close</i></span>
              <p class="header">Ano: </p>
              <p class="header">Modelo: </p>
              <p class="header">Fabricamte: </p>
              <p class="header">Cor:</p>
              <p class="card-text ini">Periodo da Reserva:<input type="text" class="flatpickr"> </p>
            </div>
            <div class="card-action">
              <a class="black-text" href="#">Reservar</a>
            </div>
          </div>
        </div>
      </div>
    </div>

  </div>
  <!-- <div class="mb-5 pb-5">
    <div class="jumbotron p-5 m-5">
      <div class="text-center p-5 m-5">
        <h1>Bem vindo!</h1>
        <p>
          Seja Bem-vindo a koyota, a maior locadora de carros da américa latina! Agora feita com Java Spring
          Boot e Vue.js!! Sinta-se a vontade para escolher um de nossos carros disponiveis para alugar.
        </p>
      </div>
    </div>
    <hr class="mb-5">
    <div class="container">
      <div class="row offset-md-1">
        <div v-for="car in carros" :key="car.id">
          <div class="col-md-4 mt-5">
            <div class="card" style="width: 18rem;">
              <div class="card-body">
                <h5 class="card-title"> {{car.nome}} </h5>
                <h6 class="card-subtitle mb-2 text-muted"> {{car.categoria}} </h6>
                <hr>
                <span class="card-text"> <b>Modelo: </b>  {{car.modelo}} </span> <br>
                <span class="card-text">  <b>Ano: </b> {{car.ano}} </span><br>
                <span class="card-text">  <b>Fabricante: </b> {{car.fabricante}} </span><br>
                <span class="card-text">  <b>Cor: </b> {{car.cor}} </span><br>
                <span class="card-text ini">  <b>Inicio: </b> <input type="date" class="form-control"> </span>
                <span class="card-text fim">  <b>Fim: </b> <input type="date" class="form-control"> </span>
                <hr>
                <a class="card-link" style="cursor: pointer" :id="car.id" @click="reservar" >Reservar</a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div> -->
</template>
<script>
$(document).ready(function(){
    M.AutoInit();
    $(".flatpickr").flatpickr({
      mode: 'range'
    });
})

$('#myModal').on('shown.bs.modal', function () {
  $('#myInput').trigger('focus')
})
import axios from 'axios'
import { mapState } from 'vuex'

  export default {
    name: 'carros',
    data() {
      return {
        carros: []
      }
    },
    
  computed: {
    ...mapState([
      'usuario',
      'logout'
    ])
  },
  methods: {
    atualizar () {
      axios.get('/carro/getAll', 
          { headers: { Accept: 'application/json' } })
        .then(res => {
          this.carros = res.data
        })
        .catch(error => console.log(error))
    },
    async reservar( e ) {

      var car;
      var usu;

      if(e.target.parentElement.children[11].children[1].value == "" || e.target.parentElement.children[12].children[1].value == "") alert("Por favor, escolha a data de inicio e fim da reserva");
      else{

        // calling object Usuario
        console.log('usuario/getById/' + this.usuario.id)
        await axios.get('usuario/getById/' + this.usuario.id)
          .then (res => {
            usu = res.data;
            // console.log('usuario:' + JSON.stringify(res.data))
          })
          .catch(error => {
            console.log(error)
          })

        await axios.get('carro/getById/' + e.target.getAttribute('id'))
          .then (res => {
            car = res.data
            // console.log("carro" + JSON.stringify(res.data))
          })
          .catch(error => {
            console.log(error)
          })

        var data = {
          usuario: usu,
          carro: car,
          data_ini: e.target.parentElement.children[11].children[1].value,
          data_fim: e.target.parentElement.children[12].children[1].value 
        }

        axios.post('reserva/save',data )
        .then(res => {
          alert('CARRO RESERVADO COM SUCESSO!');
          console.log(res.data)
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