<template>
  <div id="app">
    <h1>Jokebox</h1>
    <h2>Teste de Proficiência</h2>
    <label class="label">Name</label>
    <input class="input" type="text" placeholder="Nome" v-model="nomeField" />
    <br />
    <h3>Sobrenome</h3>
    <input type="text" placeholder="Sobrenome" v-model="sobrenomeField" />
    <br />
    <h3>E-mail</h3>
    <input type="text" placeholder="E-mail" v-model="emailField" />
    <br />
    <h3>Telefone</h3>
    <input type="number" placeholder="Telefone" v-model="telefoneField" />
    <br />
    <h3>Cnpj</h3>
    <input type="number" placeholder="numero" v-model="numeroField" />
    <br />
    <small id="nomeErro" v-show="deuErro">Estes números não são CNPJ!</small>
    <br />
    <hr />
    <div class="buttons">
    <button class="button is-warning" @click="cadastrarUsuario">Enviar</button>
        </div>

    <div v-for="(cliente, index) in orderClientes" :key="cliente.id">
      <h4>{{ index + 1}}</h4>
      <Cliente :cliente="cliente" @meDelete="deletaUsuario($event)"/>
    </div>
  </div>
</template>

<script>
import _ from 'lodash';
import Cliente from "./components/Cliente";
export default {
  name: "App",
  data() {
    return {
      deuErro: false,
      nomeField: "",
      sobrenomeField: "",
      emailField: "",
      telefoneField: "",
      numeroField: "",
      clientes: [
        {
          id: 1,
          nome: "Monalysa",
          sobrenome: "yoshikawa",
          email: "yoshikawa@gmail.com",
          telefone: "416324621456",
          cnpj: "01.852.563/0001-78"
        },
        {
          id: 2,
          nome: "Lysa",
          sobrenome: "Lysa",
          email: "lysa@gmail.com",
          telefone: "416324621456",
          cnpj: "01.852.563/0001-78"
        }
      ]
    }
  },
  components: {
    Cliente
  },
  methods: {
    cadastrarUsuario: function() {
      if(this.numeroField == "" || this.numeroField == " " || this.numeroField.length < 14 ){
        this.deuErro = true
      }else{
        this.clientes.push({
        nome: this.nomeField,
        sobrenome: this.sobrenomeField,
        email: this.emailField,
        telefone: this.telefoneField,
        cnpj: this.numeroField,
        id: Date.now()
        })
        this.nomeField= "";
        this.sobrenomeField = "";
        this.emailField = "";
        this.telefoneField = "";
        this.numeroField = "";
        this.deuErro = false;
      }
    },
    deletaUsuario: function($event){
      var id = $event.idDoCliente;
      var novoArray = this.clientes.filter(cliente => cliente.id != id);
      this.clientes = novoArray;
    }
  },
  computed: {
    orderClientes: function (){
      return _.orderBy(this.clientes,['nome'], ['asc']);
    }
  }
}
</script>

<style>
  #nomeErro {
    color: red;
  }
  #app {
    ;
  }
</style>
