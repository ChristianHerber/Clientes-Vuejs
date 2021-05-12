<template>
    <div class="card shadow" :class="{ 'bg-light': !isGold, 'border-success': isGold }">
        <div class="card-header">
            <h4>{{cliente.nome}}</h4>
        </div>
        <div class="card-body">
            <p>E-mail: {{cliente.email | processarEmail}}</p>
            <p v-if="showIdade == false">Idade: {{cliente.idade | processarIdade}}</p>
            <p v-else>Idade oculta</p>
            <span class="badge bg-warning text-dark"><small>{{idEspecial}}</small></span>
        </div>
        <div class="card-footer">
            <button class="btn btn-success btn-sm" @click="mudarCor">Aprovar</button>
            <button class="btn btn-danger btn-sm float-end" @click="emitirEventoRemover($event)">Remover</button>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                isGold: false
            }
        },
        props: {
            cliente: Object,
            showIdade: Boolean,
        },
        methods: {
            mudarCor: function() {
                this.isGold = !this.isGold
            },
            emitirEventoRemover: function() {
                this.$emit("eventoRemover", {idDoCliente: this.cliente.id})
            }
        },
        filters: {
            processarEmail: function(value){
                return value.toUpperCase()
            },
            processarIdade: function(value){
                return `${value} anos`
            }
        },
        computed: {
            idEspecial: function(){
                return (this.cliente.email + this.cliente.nome + this.cliente.id).toUpperCase()
            }
        }
    }
</script>

<style scoped>
    #cli {
        width: 20%;
        margin: 0 auto;
        padding: 15px;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        margin-bottom: 5px;
        margin-right: 5px;
        float: left;
    }
    .cliente-normal {
        background: #f7f7f7;
        color: #333;
    }

    .cliente-gold {
        background: #333;
        color: lime;
    }

</style>
