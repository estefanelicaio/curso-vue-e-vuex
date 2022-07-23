<template>
    <div class="card">
        <div class="card-header bg-dark text-white">
            <div class="row">
                <div class="col d-flex justify-content-between">
                    <div>
                        {{ titulo }}
                    </div>
                    <div>
                        <div class="form-check form-switch">
                            <input type="checkbox" class="form-check-input" v-model="favoritada">
                            <label for="form-check-label">Favoritar</label>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="card-body">
            <p>{{ descricao }}</p>
        </div>
        <div class="card-footer">
            <small class="text-muted">Salário: R${{ salario }},00 | Modalidade: {{ getModalidade }} | Tipo: {{ getTipo }} | Publicação: {{ publicacao }}</small>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Vaga',
    data: () => ({
        favoritada: false
    }),
    watch: {
        favoritada(valorNovo) {
            valorNovo ? this.emitter.emit('favoritarVaga', this.titulo) : this.emitter.emit('desfavoritarVaga', this.titulo)
        }
    },
    props: {
        titulo: {
            type: String,
            required: true,
            validator(p) {
                return p.length >= 5
            }
        }, 
        descricao: {
            type: String,
            default: 'O contratante não adicionou uma descrição para essa vaga'
        },
        salario: {
            type: Number,
            required: true
        },
        modalidade: {
            type: String,
            required: true
        },
        tipo: {
            type: String,
            required: true
        },
        publicacao: {
            type: String,
            required: true
        },
    },
    computed: {
        getModalidade() {
            switch(this.modalidade) {
                case '1': return 'Home Office'
                case '2': return 'Presencial'
            }
            return ''
        },
        getTipo() {
            switch(this.tipo) {
                case '1': return 'CLT'
                case '2': return 'PJ'
            }
            return ''
        }
    }
}
</script>