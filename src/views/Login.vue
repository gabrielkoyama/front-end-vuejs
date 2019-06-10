<template>
  <div class="row container col s6" style="margin-top: 50px">
    <div class="card-panel col s6 offset-s3">
      <form @submit.prevent="login" class="col s12">
        <h3 class="header center">Login</h3>
        <div class="input-field col s12">
          <input id="username" type="text" v-model="nome">
          <label for="username">Usuario</label>
        </div>
        <div class="input-field col s12">
          <input id="password" type="password" v-model="senha">
          <label for="password">Senha</label>
          <center>
            <button type="submit" class="waves-effect waves-light btn" style="margin: 30px">Entrar</button>
          </center>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import { mapMutations } from 'vuex'

export default {
  name: 'login',
  data() {
    return {
      nome: '',
      senha: ''
    }
  },
  
  methods: {
    ...mapMutations([
      'setUsuario',
      'setToken'
    ]),

    login() {
      axios.post('login',
          {
            username: this.nome,
            password: this.senha
          })
        .then(res => {
          console.log(res)
          this.setUsuario(res.data)
          this.setToken(res.headers.token)
          this.$router.push('/')
        })
        .catch(error => console.log(error))
    }
  }
}
</script>