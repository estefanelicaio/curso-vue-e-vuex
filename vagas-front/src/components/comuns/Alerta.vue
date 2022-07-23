<template>
    <div :class="estiloAlerta" role="alert">
        <h3>{{ titulo }}</h3>    
        <hr>
        <p>{{ descricao }}</p>
    </div>
</template>

<script>
export default {
    name: 'Alerta',
    props: {
        tipo: {
            type: String
        },
        titulo: {
            type: String
        },
        descricao: {
            type: String
        }
    },
    computed: {
        estiloAlerta() {
            switch(this.tipo) {
                case 'erro': return 'alert alert-danger'
                case 'sucesso': return 'alert alert-success'
                default: return 'alert alert-success'
            }
        }
    }
}
</script>