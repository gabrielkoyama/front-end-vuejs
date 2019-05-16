<template>
  <div>
    <div class="container">
      <form @submit.prevent="cadastrar">
        <h2>Anotação</h2>

        <div class="form-group">
          <input type="text" id="assunto" placeholder="Assunto" class="form-control col-md-5" required autofocus v-model="assunto">
        </div>

        <div class="form-group">
          <label for="texto">Texto</label>
          <textarea id="texto" class="form-control" required v-model="texto"></textarea>
        </div>

        <button class="btn btn-success" type="submit">Salvar</button>
      </form>
      
      <br>
      
      <table class="table table-striped">
        <tr>
          <th>Id</th>
          <th>Assunto</th>
          <th>Texto</th>
          <th>Data/hora</th>
          <th>Usuário</th>
        </tr>
        <tr v-for="ant in anotacoes" :key="ant.id">
          <td>{{ ant.id }}</td>
          <td>{{ ant.assunto }}</td>
          <td>{{ ant.texto }}</td>
          <td>{{ ant.dataHora }}</td>
          <td>{{ ant.usuario.nome }}</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  import {
    mapState
  } from 'vuex'

  export default {
    name: 'anotacoes',
    data() {
      return {
        assunto: '',
        texto: '',
        anotacoes: []
      }
    },
    computed: {
      ...mapState([
        'usuario'
      ])
    },
    methods: {
      cadastrar() {
        axios.post('anotacao/save', {
            assunto: this.assunto,
            texto: this.texto,
            usuario: this.usuario
          })
          .then(res => {
            this.assunto = ''
            this.texto = ''
            this.atualizar()
          })
          .catch(error => console.log(error))
      },
      atualizar() {
        axios.get('/anotacao/getAll', {
            headers: {
              Accept: 'application/json'
            }
          })
          .then(res => {
            console.log(res)
            this.anotacoes = res.data
          })
          .catch(error => console.log(error))
      }
    },
    created() {
      this.atualizar()
    }
  }
</script>