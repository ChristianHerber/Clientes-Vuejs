<template>
    <div class="card shadow" :class="{ 'bg-light': !isGold, 'border-success': isGold }">
        <div class="card-header">
            <h4>{{cliente.nome}}</h4>
        </div>
        <div class="card-body">
            <p>E-mail: {{cliente.email}}</p>
            <p v-if="showIdade == false">Idade: {{cliente.idade}}</p>
            <p v-else>Idade oculta</p>
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
