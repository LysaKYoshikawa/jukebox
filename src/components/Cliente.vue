<template>
    <div id= "Cliente">
    <h4>Nome: {{cliente.nome}}</h4>
    <p>Sobrenome: {{cliente.sobrenome}}</p>
    <p>E-mail: {{cliente.email}}</p>
    <p>Telefone: {{cliente.telefone}}</p>
    <p v-if="showCnpj === true" >Cnpj: {{cliente.cnpj}}</p> 
    <p v-else></p>
    <div>
        <button class="button is-warning"  @click="emitirEventoDelete">Deletar</button>
    </div>

    </div>

</template>

<script>
export default {
    data() {

        return {     
        }
    },

    props: {
        
        cliente: Object,
        showCnpj: Boolean
        
    },
    methods: {
        emitirEventoDelete: function(){
            console.log("Emitindo do filho!");
            this.$$emit("meDelete", {idDoCliente: this.cliente.id,curso:"Formação node.js", emPromocao: true, component: this});
        },     

    }
    
}
</script>

<style scoped>
    #Cliente{
        color:blue;
        background: burlywood;
    }

</style>