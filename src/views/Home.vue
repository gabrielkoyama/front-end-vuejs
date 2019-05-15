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
      <div class="row">
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
                <hr>
                <a href="#" class="card-link">Reservar</a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
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
      console.log('fazendo a requisição')
      axios.get('/carro/getAll', 
          { headers: { Accept: 'application/json' } })
        .then(res => {
          console.log(res)
          this.carros = res.data
        })
        .catch(error => console.log(error))
    }
  },
  created () {
    console.log('chamando o chamador da requisição')
    this.atualizar()
  }
}
</script>
