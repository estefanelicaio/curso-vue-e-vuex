<template>
    <i v-for="estrela in estrelas" :key="estrela.id" :class="estrela.estilo" @click="marcarAvaliacao(estrela.id)"></i>
</template>

<script>
export default {
    name: "InputEstrelas",
    props: {
        numeroEstrelas: {
            type: Number,
            required: true
        }
    },
    data: () => ({
        estrelas: [],
        avaliacao: 0
    }),
    created() {
        this.iniciarEstrelas()
    },
    methods: {
        iniciarEstrelas() {
            for(let i = 0; i < this.numeroEstrelas; i++) {
                this.estrelas[i] = {id: i, estilo: 'bi-star estrela'}
            }
        },
        marcarAvaliacao(avaliacao) {
            this.iniciarEstrelas()

            this.avaliacao = ++avaliacao

            for(let i = 0; i < avaliacao; i++) {
                this.estrelas[i].estilo = 'bi-star-fill estrela preenchida'
            }

            // this.$emit('avaliar', this.avaliacao)
            this.$emit('update:avaliar', this.avaliacao)
        }
    }
}
</script>

<style scoped>

.estrela {
    font-size: 1.5rem;
    color: #999;
    cursor: pointer;
}

.preenchida {
    color: #000;
}

</style>