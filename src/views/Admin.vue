<template>
  <div class="m-5" style="border-radius: 10px" id="">

    <samp> Visão Geral</samp>

    <div class="row offset-md-2">
          <div class="col-md-3 grid-margin stretch-card">
            <div class="card">
              <div class="card-body">
                <p class="card-title text-md-center text-xl-left">USUARIOS</p>
                <div class="d-flex flex-wrap justify-content-between justify-content-md-center justify-content-xl-between align-items-center">
                  <h3 class="mb-0 mb-md-2 mb-xl-0 order-md-1 order-xl-0 pb-3">2</h3>
                  <i class="ti-calendar icon-md text-muted mb-0 mb-md-3 mb-xl-0"></i>
                </div>  
                <!-- <p class="mb-0 mt-2 text-danger">0.12% <span class="text-black ml-1"><small>(30 days)</small></span></p> -->
              </div>
            </div>
          </div>
          <div class="col-md-3 grid-margin stretch-card">
            <div class="card">
              <div class="card-body">
                <p class="card-title text-md-center text-xl-left">Carros</p>
                <div class="d-flex flex-wrap justify-content-between justify-content-md-center justify-content-xl-between align-items-center">
                  <h3 class="mb-0 mb-md-2 mb-xl-0 order-md-1 order-xl-0 pb-3">3</h3>
                  <i class="ti-user icon-md text-muted mb-0 mb-md-3 mb-xl-0"></i>
                </div>  
                <!-- <p class="mb-0 mt-2 text-danger">0.47% <span class="text-black ml-1"><small>(30 days)</small></span></p> -->
              </div>
            </div>
          </div>
          <div class="col-md-3 grid-margin stretch-card">
            <div class="card">
              <div class="card-body">
                <p class="card-title text-md-center text-xl-left">Reservas</p>
                <div class="d-flex flex-wrap justify-content-between justify-content-md-center justify-content-xl-between align-items-center">
                  <h3 class="mb-0 mb-md-2 mb-xl-0 order-md-1 order-xl-0 pb-3">400</h3>
                  <i class="ti-agenda icon-md text-muted mb-0 mb-md-3 mb-xl-0"></i>
                </div>  
                <!-- <p class="mb-0 mt-2 text-success">64.00%<span class="text-black ml-1"><small>(30 days)</small></span></p> -->
              </div>
            </div>
          </div>
        
        </div>


    <hr class="mt-5 mb-5">

    <!-- CARRO -->
    <div class="car1d">
			<div class="card-body p-0">
				<h5 class="card-title" style="margin: 10px 10px 0px 10px; padding: 0.65rem; ">
					<span>
						Carros
					</span>
          <span class="float-right" style="font-size: 14px">
            <a href="" data-toggle="modal" data-target="#modal_carro"><i class="fas fa-plus fa-xs"></i> Novo carro</a>
          </span>
				<div class="dropdown-divider"></div>
				</h5>
        <div class="container">
					<table class="table table-stripped mt-2 carros">
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
                <!-- <th></th> -->
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
                <!-- <td> <a style="cursor: pointer"> <i class="fas fa-edit fa-sm"></i> </a> </td> -->
                <td> <a style="cursor: pointer" :id="car.id" @click="deleteCarById"> <i class="fas fa-trash fa-sm" style="color: red"></i> </a> </td>
              </tr>
            </tbody>
          </table>
        </div>
			</div>
		</div>
    <hr class="mt-5 mb-5">
    
    <!-- USUARIO -->
    <div class="car1d">
			<div class="card-body p-0">
				<h5 class="card-title" style="margin: 10px 10px 0px 10px; padding: 0.65rem; ">
					<span>
						Usuarios
					</span>
          <span class="float-right" style="font-size: 14px">
            <a href="" data-toggle="modal" data-target="#modal_usuario"><i class="fas fa-plus fa-xs"></i> Novo usuario</a>
          </span>
				<div class="dropdown-divider"></div>
				</h5>
        <div class="container">
					<table class="table table-stripped mt-2 usuarios">
            <thead>
              <tr>
                <th> Nome </th>
                <th> Cpf </th>
                <th> Telefone </th>
                <th> Autorização </th>
                <!-- <th></th> -->
                <th></th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="usu in usuarios" :key="usu.id">
                <td>{{usu.nome}}</td>
                <td>{{usu.cpf}}</td>
                <td>{{usu.telefone}}</td>
                <td>{{usu.autorizacoes.length}}</td>
                <!-- <td> <a href=""> <i class="fas fa-edit fa-sm"></i> </a> </td> -->
                <td> <a style="cursor: pointer" :id="usu.id" @click="deleteUsuarioById"> <i class="fas fa-trash fa-sm"></i> </a> </td>
              </tr>
            </tbody>
          </table>
        </div>
			</div>
		</div>

    <hr class="mt-5 mb-5">
    
    <!-- RESERVA -->

    <div class="car1d">
			<div class="card-body p-0">
				<h5 class="card-title" style="margin: 10px 10px 0px 10px; padding: 0.65rem; ">
					<span>
						Reservas
					</span>
          <span class="float-right" style="font-size: 14px">
            <a href=""><i class="fas fa-plus fa-xs"></i> Novo carro</a>
          </span>
				<div class="dropdown-divider"></div>
				</h5>
        <div class="container">
					<table class="table table-stripped mt-2 carros">
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
                <!-- <th></th> -->
                <th></th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>a</td>
                <td>a</td>
                <td>a</td>
                <td>a</td>
                <td>a</td>
                <td>a</td>
                <td>a</td>
                <td>a</td>
                <!-- <td> <a href=""> <i class="fas fa-edit fa-sm"></i> </a> </td> -->
                <td> <a href=""> <i class="fas fa-trash fa-sm"></i> </a> </td>
              </tr>
              
            </tbody>
          </table>
        </div>
			</div>
		</div>

    <!-- MODAL CARRO -->
    <div class="modal fade" id="modal_carro" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog" role="document">
        <div class="modal-content" style="wid1th: 800px;">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Cadastrar Novo Carro</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
            <form class="form" @submit.prevent="addCar">
              <div class="modal-body">
                <div class="form-group">
                  <label>Nome</label>
                  <input type="text" class="form-control" v-model="car_nome">
                </div>
                <div class="form-group">
                  <label>Categoria</label>
                  <input type="text" class="form-control" v-model="car_km">
                </div>
                <div class="form-group">
                  <label>Km</label>
                  <input type="text" class="form-control" v-model="car_categoria">
                </div>
                <div class="form-group">
                  <label >Modelo</label>
                  <input type="text" class="form-control" v-model="car_modelo">
                </div>
                <div class="form-group">
                  <label >Ano</label>
                  <input type="text" class="form-control" v-model="car_ano" >
                </div>

                <div class="form-group">
                  <label >Fabricante</label>
                  <input type="text" class="form-control" v-model="car_fabricante" >
                </div>

                <div class="form-group">
                  <label >Cor</label>
                  <input type="text" class="form-control" v-model="car_cor" >
                </div>
              </div>
              <div class="modal-footer">
                <button type="submit" class="btn btn-sm btn-primary">Save changes</button>
              </div>
            </form>
        </div>
      </div>
    </div>

    <!-- MODAL USUARIO -->
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

<script>

import axios from 'axios'
import { mapState } from 'vuex'

var global = 0;

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
          alert('CARRO CADASTRADO COM SUCESSO');
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
          alert('USUARIO CADASTRADO COM SUCESSO');
          this.atualizar()
        })
        .catch(error => console.log(error))
    },
    async atualizar () {
      // console.log('CALLING CARRO GET ALL')
      await axios.get('/carro/getAll', 
          { headers: { Accept: 'application/json' } })
        .then( async res  => {
          this.carros = res.data;
        })
        .catch(error => console.log(error))
      
      // console.log('CALLING RESERVA GET ALL')
      await axios.get('/reserva/getAll', 
          { headers: { Accept: 'application/json' } })
        .then(res => {
          this.reservas = res.data
        })
        .catch(error => console.log(error))
      
      // console.log('CALLING USUARIO GET ALL')
      await axios.get('/usuario/getAll', 
          { headers: { Accept: 'application/json' } })
        .then(res => {
         console.log(res.data.au)
          this.usuarios = res.data
        })
        .catch(error => console.log(error))

      // espera os 'ajax' rodarem pra depois montar a table
      $('.carros').DataTable();
      $('.reservas').DataTable();
      $('.usuarios').DataTable();
    },
    deleteCarById ( e ) {
      var id = e.target.parentElement.getAttribute('id')
      console.log(id)
      axios.delete('/carro/deleteById/' + id, 
          { headers: { Accept: 'application/json' } })
        .then(res => {
          alert('DELETADO COM SUCESSO!');
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
        alert('DELETADO COM SUCESSO!');
        // location.reload();
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