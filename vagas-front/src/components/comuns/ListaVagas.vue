<template>
    <slot :vagas="vagas">
        <div class="row mt-5" v-for="(vaga, index) in vagas" :key="index">
            <div class="col">
                <vaga v-bind="vaga"/>
            </div>
        </div>
    </slot>
</template>

<script>
import Vaga from '@/components/comuns/Vaga.vue';

export default {
    name: 'ListaVagas',
    data: () => ({
        vagas: []
    }),
    components: {
        Vaga
    },
    mounted() {
        this.emitter.on('filtrarVagas', vaga => {
            
            const vagas = JSON.parse(localStorage.getItem('vagas'))
            this.vagas = vagas.filter(item => item.titulo.toLowerCase().includes(vaga.titulo.toLowerCase()))
        })
    },
    activated() {
        this.vagas = JSON.parse(localStorage.getItem('vagas'))
    }
}
</script>