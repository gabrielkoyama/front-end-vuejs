<template>
  <div>
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
 
<!--      <div class="col-md-4 mt-5">
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
        <div class="col s12 m4" v-repeat="car in carros" :key="car.id">
          <div class="card hoverable" style="overflow: visible;">
            <div class="card-image waves-effect waves-block waves-light" style="padding: 20px !important">
              <img class="activator" src="assets/img/car_example_1.png">
            </div>
            <div class="card-content">
              <span class="card-title activator grey-text text-darken-4">Nome do carro<i class="material-icons right">more_vert</i></span>
            </div>
            <div class="card-reveal" style="display: none; transform: translateY(0%);">
              <span class="card-title grey-text text-darken-4">Informações<i class="material-icons right">close</i></span>
              <p class="header">Ano: {{car.ano}} </p>
              <p class="header">Modelo: {{car.modelo}} </p>
              <p class="header">Fabricamte: {{car.fabricante}} </p>
              <p class="header">Cor: {{car.cor}} </p>
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
import { mapMutations } from 'vuex'

  export default {
    name: 'carros',
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