<template>
  <div id="app">
    <div id="nav">
      <div class="d-flex flex-column flex-md-row align-items-center p-3 px-md-4 mb-3 bg-white border-bottom shadow-sm">
        <h4 class="my-0 mr-md-auto font-weight-normal"> <i>Koyota</i></h4>
        <nav class="my-2 my-md-0 mr-md-3">

          <a href="#"><router-link class="p-2 text-dark" to="/">Home</router-link></a>
          <a  v-if="usuario" href="#"><router-link class="p-2 text-dark" to="/admin">Admin</router-link> </a>
          <a class="p-2 text-dark" href="#"><router-link class="p-2 text-dark" v-if="!usuario" to="/login">Login</router-link></a>
          <a class="p-2 text-dark" href="#"><a class="p-2 text-dark" v-if="usuario" @click="logout">Logout</a> </a>
        </nav>
        <!-- <a class="btn btn-sm btn-outline-dark" href="#">Sign up</a> -->
      </div>
    </div>
    <router-view/>
  </div>
</template>

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
