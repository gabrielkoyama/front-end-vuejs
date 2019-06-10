<template>
  <div id="app">
    <div id="nav">
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
    </div>
    <router-view/>
  </div>
</template>
<style>

  .nav-item:hover{
    color: rgba(255, 0, 0, 0.849);
    background-color: #fafafa0a;
    transition: 0.7s;
  }

  .img {
    background-image: url('/public/assets/img/wpp_car_1.jpg')
  }

</style>
<script>
import { mapState } from 'vuex'
import { mapMutations } from 'vuex'

export default {
  name: 'app',
  computed: {
    ...mapState([
      'usuario'
    ])
  },
  methods: {
    ...mapMutations([
      'logout'
    ])
  }
}
</script>
