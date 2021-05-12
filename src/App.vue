<template>
  <div id="app">
    <div class="container">
      <div class="row">

        <div class="col-md-6 offset-md-3">
          <div class="form">
            <div class="text-danger nomeErro" v-show="nomeErro"><small>Nome inválido, preencha corretamente!</small></div>
            <input class="form-control" type="text" placeholder="nome" v-model="nomeField">
            <input class="form-control" type="email" placeholder="seu@email.com" v-model="emailField">
            <input class="form-control" type="number" placeholder="idade" v-model="idadeField">
            <button class="btn btn-primary" @click="cadastrarUsuario">Cadastrar</button>
          </div>
        </div>

        <div class="col-md-12">
          <div class="row">
            <div class="col-md-4 mb-4" v-for="cliente in clientes" :key="cliente.id">
              <Cliente :cliente="cliente" @eventoRemover="removerUsuario($event)"/>
            </div>
          </div>
        </div>

      </div> <!-- row -->
    </div> <!-- container -->
    
  </div>
</template>

<script>
// import { component } from 'vue/types/umd'
import Cliente from './components/Cliente'
// import Produto from './components/Produto'

export default {
  name: 'App',
  data(){
    return {
      nomeErro: false,
      nomeField: "",
      emailField: "",
      idadeField: "",
      clientes:[]
    }
  },
  components: {
    Cliente,
  },
  methods: {
    cadastrarUsuario: function(){
      if(this.nomeField.length < 3){
        this.nomeErro = true
      } else {
        this.clientes.push({nome: this.nomeField, email: this.emailField, idade: this.idadeField, id: Date.now()})
        
        this.nomeField = ""
        this.emailField = ""
        this.idadeField = 0

        this.nomeErro = false
      }
    },
    removerUsuario: function($event){
      let id = $event.idDoCliente
      let novoArray = this.clientes.filter(cliente => cliente.id != id)
      this.clientes = novoArray
    }
  },
}

</script>

<style>
  #app {
    width: 100%;
  }
  .form {
    width: 100%;
    padding: 15px;
    margin: 5px 0;
  }
  .form input {
    margin-bottom: 5px;
  }
</style>
