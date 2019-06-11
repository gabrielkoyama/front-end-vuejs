<template>
  <div>
    <nav style="background-color: black">
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
  </div>
</template>

<script>
  import axios from 'axios'
  import { mapState } from 'vuex'
  import { mapMutations } from 'vuex'


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
      ...mapMutations([
        'logout'
      ]),
      async atualizar(){
        var hj = new Date()
        await axios.get('/reserva/getAll/',
          { headers: { Accept: 'application/json' } })
        .then(res => {
          res.data.filter(( e )=> { return e.usuario.id == this.usuario.id ? this.reserva.push(e) : console.log(''); });
        })
        .catch(error => console.log(error))
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