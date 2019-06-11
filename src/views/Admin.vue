<template>

  <div class="m-5" style="border-radius: 10px; background-color: #ccc" id="">
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
    <h5 class="header center"> Visão Geral</h5>
    <div class="row container">
      <div class="col s12 m4">
        <div class="card hoverable">
          <div class="card-content">
            <span class="card-title">
              Usuarios
              <i class="material-icons">group</i>
            </span>
            <p> {{usuarios.length}} </p>            
          </div>
        </div>
      </div>

      <div class="col s12 m4">
        <div class="card hoverable">
          <div class="card-content">
            <span class="card-title">Carros <i class="material-icons">directions_car</i></span>
            <p> {{carros.length}} </p>            
          </div>
        </div>
      </div>

      <div class="col s12 m4">
        <div class="card hoverable">
          <div class="card-content">
            <span class="card-title">Reservas <i class="material-icons">insert_emoticon</i></span>
            <p> {{reservas.length}} </p>            
          </div>
        </div>
      </div>
    </div>

    <h5 class="header center space"> Carros </h5>
    <div class="container">
      <div class="card hoverable">
          <div class="card-content">
            <table class="table striped highlight">
              <thead>
                <tr>
                  <th> Nome </th>
                  <th> Km </th>
                  <th> Categoria </th>
                  <th> Modelo </th>
                  <th> Ano </th>
                  <th> Fabricante </th>
                  <th> Cor </th>
                  <th> Disponivel </th>
                  <th></th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="car in carros" :key="car.id">
                  <td>{{car.nome}}</td>
                  <td>{{car.km}}</td>
                  <td>{{car.categoria}}</td>
                  <td>{{car.modelo}}</td>
                  <td>{{car.ano}}</td>
                  <td>{{car.fabricante}}</td>
                  <td>{{car.cor}}</td>
                  <td>{{car.disponivel}}</td>
                  <td> <a style="cursor: pointer" :id="car.id" @click="deleteCarById"> <i class="material-icons" style="color: red">delete_forever</i> </a> </td>
                </tr>
              </tbody>
          </table>
          </div>
      </div>
    </div>
    
    <h5 class="header center space"> Usuários </h5>
    <div class="container">
    <div class="card hoverable">
        <div class="card-content">
          <table class="table striped highlight">
            <thead>
              <tr>
                <th> Nome </th>
                <th> Cpf </th>
                <th> Telefone </th>
                <th> Autorização </th>
                <th></th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="usu in usuarios" :key="usu.id">
                <td>{{usu.nome}}</td>
                <td>{{usu.cpf}}</td>
                <td>{{usu.telefone}}</td>
                <td>{{usu.autorizacoes.length}}</td>
                <td> <a style="cursor: pointer" :id="usu.id" @click="deleteUsuarioById"> <i class="material-icons" style="color: red">delete_forever</i></a> </td>
              </tr>
            </tbody>
          </table>
        </div>
    </div>
  </div>


  <h5 class="header center space"> Reservas </h5>
  <div class="container" style="padding-bottom: 50px">
    <div class="card hoverable">
        <div class="card-content">
          <table class="table striped highlight">
            <thead>
              <tr>
                <th> Nome </th>
                <th> Cpf </th>
                <th> Teelfone </th>
                <th> Carro </th>
                <th> Modelo </th>
                <th> Data Inicio </th>
                <th> Data Fim </th>
                <th></th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="rsv in reservas" :key="rsv.id">
                <td>{{rsv.usuario.nome}}</td>
                <td>{{rsv.usuario.cpf}}</td>
                <td>{{rsv.usuario.telefone}}</td>
                <td>{{rsv.carro.nome}}</td>
                <td>{{rsv.carro.modelo}}</td>
                <td>{{rsv.data_ini}}</td>
                <td>{{rsv.data_fim}}</td>
                <td> <a style="cursor: pointer" :id="rsv.id" @click="deleteReservaById"><i class="material-icons" style="color: red">delete_forever</i> </a> </td>
              </tr>
            </tbody>
          </table>
        </div>
    </div>
  </div>

  <div class="fixed-action-btn">
    <a class="btn-floating btn-large black">
      <i class="large material-icons">add</i>
    </a>
    <ul>
      <li><a href="#new_car" class="btn-floating red modal-trigger"><i class="material-icons tooltipped" data-position="left" data-tooltip="Novo usuário">group</i></a></li>
      <li><a href="#new_usr" class="btn-floating yellow darken-1 modal-trigger"><i class="material-icons tooltipped" data-position="left" data-tooltip="Novo carro">directions_car</i></a></li>
    </ul>
  </div>

  <div id="new_car" class="modal">
    <div class="modal-content">
      <h5 class="header center">Cadastrar Novo Carro</h5>
      
      <form class="form" @submit.prevent="addCar">

        <div class="input-field col s12">
          <input id="username" type="text" v-model="car_nome">
          <label for="username">Nome</label>
        </div>

        <div class="input-field col s12">
          <input id="username" type="text" v-model="car_categoria">
          <label for="username">Categoria</label>
        </div>

        <div class="input-field col s12">
          <input id="username" type="text" v-model="car_km">
          <label for="username">Km</label>
        </div>

        <div class="input-field col s12">
          <input id="username" type="text" v-model="car_modelo">
          <label for="username">Modelo</label>
        </div>

        <div class="input-field col s12">
          <input id="username" type="text" v-model="car_ano">
          <label for="username">Ano</label>
        </div>

        <div class="input-field col s12">
          <input id="username" type="text" v-model="car_fabricante">
          <label for="username">Fabricante</label>
        </div>

        <div class="input-field col s12">
          <input id="username" type="text" v-model="car_cor">
          <label for="username">Cor</label>
        </div>
        <button type="submit" style="float: right" class="modal-close waves-effect waves-green btn-flat">Cadastrar</button>
      </form>
    </div>
  </div>

  <div id="new_usr" class="modal">
    <div class="modal-content">
      <h5 class="header center">Cadastrar novo usuário</h5>
        <form class="form" @submit.prevent="addUser">

          <div class="input-field col s12">
            <input id="username" type="text" v-model="usr_nome">
            <label for="username">Nome</label>
          </div>

          <div class="input-field col s12">
            <input id="username" type="text" v-model="usr_psw">
            <label for="username">Senha</label>
          </div>

          <div class="input-field col s12">
            <input id="username" type="text" v-model="usr_cpf">
            <label for="username">Cpf</label>
          </div>

          <div class="input-field col s12">
            <input id="username" type="text" v-model="usr_tel">
            <label for="username">Telefone</label>
          </div>

          <div class="input-field col s12">
            <select v-model="usr_aut">
              <option value="" disabled selected>Choose your user role</option>
              <option value="ROLE_ADMIN">ADMIN</option>
              <option value="ROLE_USUARIO">USUARIO</option>
            </select>
          </div>
          <button type="submit" style="float: right" class="modal-close waves-effect waves-green btn-medium btn-flat">Cadastrar</button>
        </form>
    </div>
  </div>

  <a hidden id="success_del" onclick="M.toast({html: 'Deletado com sucesso!'})"></a>
  <a hidden id="success_add" onclick="M.toast({html: 'Cadastrado com sucesso!'})"></a>
    
   
    <div class="modal fade" id="modal_usuario" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog" role="document">
        <div class="modal-content" style="wid1th: 800px;">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Cadastrar Novo Usuario</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
            <form class="form" @submit.prevent="addUser">
              <div class="modal-body">
                <div class="form-group">
                  <label>Nome</label>
                  <input type="text" class="form-control" v-model="usr_nome">
                </div>
                <div class="form-group">
                  <label>Senha</label>
                  <input type="text" class="form-control" v-model="usr_psw">
                </div>
                <div class="form-group">
                  <label>Cpf</label>
                  <input type="text" class="form-control" v-model="usr_cpf">
                </div>
                <div class="form-group">
                  <label>Telefone</label>
                  <input type="text" class="form-control" v-model="usr_tel">
                </div>
                <div class="form-group">
                  <label>Autorização</label>
                  <select class="form-control" name="" id="" v-model="usr_aut" >
                    <option value="ROLE_ADMIN">ADMIN</option>
                    <option value="ROLE_USUARIO">USUARIO</option>
                  </select>
                </div>
              </div>
              <div class="modal-footer">
                <button type="submit" class="btn btn-sm btn-primary">Cadastrar</button>
              </div>
            </form>
        </div>
      </div>
    </div>
  </div>
</template>

<style>

  .space {
    padding: 20px;
  }

</style>


<script>

$(document).ready(function(){
  $('.fixed-action-btn').floatingActionButton();
  $('.tooltipped').tooltip();
  $('.modal').modal();
  $('select').formSelect();
})

import axios from 'axios'
import { mapState } from 'vuex'
import { mapMutations } from 'vuex'


var global = 0;
var teste;

export default {
  name: 'admin',
  data() {
    return {
      
      // carro
      car_nome: null,
      car_km: null,
      car_categoria:null,
      car_modelo:null,
      car_ano:null,
      car_fabricante:null,
      car_cor:null,
      car_disponivel:null,

      // usuario
      usr_nome: null,
      usr_cpf: null,
      usr_tel:null,
      usr_aut:null,
      usr_psw:null,

      reservas: [],
      usuarios: [],
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
    async atualizar () {
      await axios.get('/carro/getAll', 
          { headers: { Accept: 'application/json' } })
        .then( async res  => {
          this.carros = res.data;
        })
        .catch(error => console.log(error))

      await axios.get('/usuario/getAll', 
          { headers: { Accept: 'application/json' } })
        .then(res => {
         console.log(res.data.au)
          this.usuarios = res.data
          teste = res.data
        })
        .catch(error => console.log(error))
      
      await axios.get('/reserva/getAll', 
          { headers: { Accept: 'application/json' } })
        .then(res => {
          console.log(res.data)
          this.reservas = res.data
        })
        .catch(error => console.log(error))
      
      // $('.carros').DataTable();
      // $('.usuarios').DataTable();
      // $('.reservas').DataTable();
    },
    addCar() {

      var data = {
        nome: this.car_nome,
        km: this.car_km,
        categoria: this.car_categoria,
        modelo: this.car_modelo,
        ano: this.car_ano,
        fabricante: this.car_fabricante,
        cor: this.car_cor,
        disponivel: true
      }
      
      console.log(data)

      axios.post('carro/save', data )
        .then(res => {
          // alert('CARRO CADASTRADO COM SUCESSO');
          $('#success_add').click()
          this.atualizar()
        })
        .catch(error => console.log(error))
    },
    addUser(){
      var autObject;
      //mount autorization workaround
      if(this.usr_aut == 'ROLE_ADMIN') autObject = [{id:1, nome:this.usr_aut, authority: this.usr_aut}]
      if(this.usr_aut == 'ROLE_USUARIO') autObject = [{id:2, nome:this.usr_aut, authority: this.usr_aut}]
      var data = {
        nome: this.usr_nome,
        senha: "{MD5}698dc19d489c4e4db73e28a713eab07b",
        cpf: this.usr_cpf,
        autorizacoes: autObject,
        telefone: this.usr_tel
      }
      console.log(JSON.stringify(data));
      axios.post('usuario/save', data )
        .then(res => {
          // alert('USUARIO CADASTRADO COM SUCESSO');
          $('#success_add').click()
          this.atualizar()
        })
        .catch(error => console.log(error))
    },
    deleteCarById ( e ) {
      var id = e.target.parentElement.getAttribute('id')
      console.log(id)
      axios.delete('/carro/deleteById/' + id, 
          { headers: { Accept: 'application/json' } })
        .then(res => {
          // alert('DELETADO COM SUCESSO!');
          $('#success_del').click()
          this.atualizar()
          console.log('res');
        })
        .catch(error => console.log(error))
    },
    deleteUsuarioById( e ){
      var id = e.target.parentElement.getAttribute('id');
      console.log(id)
      axios.delete('/usuario/deleteById/' + id,
          { headers: { Accept: 'application/json' } })
        .then(res => {
          // alert('DELETADO COM SUCESSO!');
          $('#success_del').click()
          this.atualizar()
          console.log('res');
        })
        .catch(error => console.log(error))
    },
    deleteReservaById( e ){
      var id = e.target.parentElement.getAttribute('id');
      console.log(id)
      axios.delete('/reserva/deleteById/' + id,
          { headers: { Accept: 'application/json' } })
        .then(res => {
          // alert('DELETADO COM SUCESSO!');
          $('#success_del').click()
          this.atualizar()
          console.log('res');
        })
        .catch(error => console.log(error))
    }
  },
  created () {
    this.atualizar()
  }
}
</script>