<template>
    <div :class="{'cliente' : !isPremium, 'cliente-premium':isPremium}">
    <h1 >{{cliente.nome}}</h1>
    <h2>{{cliente.codigo, | processarCodigo}}</h2>
    <h2>{{cliente.veiculo}}</h2>
    <h2>{{cliente.placa}}</h2>
    <h2>{{cliente.cor}}</h2>
    <h2 v-if="showContato === false">{{cliente.contato}}</h2>
    <h2 v-else>Usuario escondeu o contato</h2>
    <button @click="mudarCor($event)">Rodando</button>
    <button @click="emitirEventoDelete">Deletar</button>
    <h4>idEspecial:{{idEspecial}}</h4>
    </div>
</template>
<script>
export default {
      data(){
    return{
        isPremium: true
      
      }
    },
    props:{
        cliente:Object,
        showContato:Boolean
    },
    methods:{
        mudarCor: function($event){
            console.log($event);
        this.isPremium = !this.isPremium
        },
        emitirEventoDelete: function(){
            console.log("Emitindo do filho");
            this.$emit("meDelete",{idDoCliente:this.cliente.id,curso:"Formaçao node.js", emPromocao: true, component: this});
        }

        },
        computed:{
            idEspecial: function(){
            return(this.cliente.codigo + this.cliente.nome).toUpperCase();
        }
        


    }
    
    
}
</script>
<style scoped>
.cliente{
    color: rgb(2, 2, 2);
    background: rgb(80, 255, 95);
}
.cliente-premium{
    color: rgb(247, 247, 247);
    background: rgb(10, 10, 10);
}


</style>