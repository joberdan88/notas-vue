<template>
    <div class="nota">
        <p :class="{ riscado: concluida }">{{ texto }}</p>

        <div class="botoes">
            <button @click="$emit('concluir')">✔️</button>
            <button @click="editando = !editando">✏️</button>
            <button @click="$emit('remover')">🗑️</button>
        </div>

        <div v-if="editando">
            <input v-model="novoTexto" @keyup.enter="confirmarEdicao" />
            <button @click="confirmarEdicao">Salvar</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'NotaItem',
    props: ['texto', 'concluida'],
    data() {
        return {
            editando: false,
            novoTexto: this.texto
        }
    },
    methods: {
        confirmarEdicao() {
            this.$emit('editar', this.novoTexto.trim())
            this.editando = false
        }
    }
}
</script>

<style scoped>
.nota {
    background-color: #f9f9f9;
    border: 1px solid #ddd;
    padding: 15px;
    position: relative;
}
.riscado {
    text-decoration: line-through;
    color: #888;
}
.botoes {
    display: flex;
    gap: 10px;
    margin-top: 10px;
}
input {
    width: 100%;
    padding: 5px;
    margin-top: 10px;
}
</style>

