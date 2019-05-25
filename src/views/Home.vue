<template>
  <div class="mb-5 pb-5">
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
  </div>
</template>


<script>
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
      'usuario'
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