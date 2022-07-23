<template>
    <div>
        <vagas-favoritas></vagas-favoritas>
        <topo-padrao @navegar="componente = $event"/>
        <alerta v-if="exibirAlerta" :tipo="alerta.tipo" :titulo="alerta.titulo" :descricao="alerta.descricao"/>
        <Conteudo :conteudo="componente"></Conteudo>
    </div> 
</template>

<script>
import Conteudo from '@/components/layouts/Conteudo.vue';
import TopoPadrao from '@/components/layouts/TopoPadrao.vue';
import VagasFavoritas from '@/components/comuns/VagasFavoritas.vue';
import Alerta from '@/components/comuns/Alerta.vue';

export default {
  name: 'App',
  data: () => ({
    componente: 'home',
    exibirAlerta: false,
    alerta: { tipo: '', titulo: '', descricao: '' }
  }),
  components: {
    Conteudo,
    TopoPadrao,
    VagasFavoritas,
    Alerta
  },
  mounted() {
    this.emitter.on('alerta', (a) => {
        this.alerta = a
        this.exibirAlerta = true
        setTimeout(() => this.exibirAlerta = false, 4000)
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
