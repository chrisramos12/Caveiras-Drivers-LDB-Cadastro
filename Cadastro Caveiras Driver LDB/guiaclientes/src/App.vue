<template>
  <div id="app"> 
    <h3>Cadastro:</h3>
    <div class="buttons">
  <button class="button is-primary">Primary</button>
  <button class="button is-link">Link</button>
</div>
    <small id="erroDeValidacao" v-show="deuErro">Erro de validação tente novamente!</small><br>
    <input type="text" placeholder="nome" v-model="nomeField"><br>
    <input type="text" placeholder="codigo" v-model="codigoField"><br>
    <input type="text" placeholder="veiculo" v-model="veiculoField"><br>
    <input type="text" placeholder="cor" v-model="corField"><br>
    <input type="text" placeholder="placa" v-model="placaField"><br>
    <input type="text" placeholder="contato" v-model="contatoField"><br>
    <button @click="cadastrarClientes">Cadastrar</button>
    <hr>
    <hr>

 <div v-for="(cliente, index) in orderClientes" :key="cliente.id">
   <h4>{{index+1}}</h4>
  <Cliente :cliente="cliente" @meDelete="deletarUsuario($event)"/>

  <hr>

 </div>
  </div>
</template>


<script>
import _ from 'lodash';
import Cliente from './components/Cliente.vue'
//import Produto from './components/Produto.vue'

export default {

  
  name: 'App',
  data(){
    return{
      deuErro: false,
      nomeField:"",
      codigoField:"",
      veiculoField:"",
      corField:"",
      placaField:"",
      contatoField:"",

    clientes:[
      {
      id:2,
      nome:"Christian Ramos",
      veiculo:"Mobi",
      codigo:"C138",
      cor: "Branco",
      contato:"93929292"
      },
      {
      nome:"Chris Ramos",
      veiculo:"Gol",
      codigo:"C139",
      cor: "Preto",
      contato:"84433848"
      },
      {
        id:3,
      nome:"Christian",
      veiculo:"Ka",
      codigo:"C140",
      cor: "Prata",
      contato:"9399292"
      }
    ]

    
    }
  },
  components:{
    Cliente,
    //Produto   
  },
  methods:{
    cadastrarClientes: function(){
      if(this.codigoField<2|| this.nomeField<3||this.veiculoField<3||this.corField<3||this.placaField<3){
        this.deuErro=true;
      }else{

    this.clientes.push({nome: this.nomeField,codigo: this.codigoField, veiculo: this.veiculoField,
    cor: this.corField, placa: this.placaField, contato: this.contatoField, id: Date.now()})
    this.nomeField = "",
    this.codigoField="",
    this.veiculoField="",
    this.corField="",
    this.placaField="",
    this.contatoField=""
    this.deuErro=false;
      } 
    },
    deletarUsuario: function($event){
      console.log("Recebendo evento");
      var id = $event.idDoCliente;
      var novoArray = this.clientes.filter(cliente => cliente.id != id);
      this.clientes = novoArray;
    }
  },
  computed:{
    orderClientes: function(){
      return _.orderBy(this.clientes,['codigo',['asc']]);
    }
  }


}
</script>

<style>
  #erroDeValidacao{
    color:red;
  }
</style>
