<template>
    <div id="app" class="container">
        <h1> Minhas Notas</h1>
        <input v-model="novaNota" @keyup.enter="adicionarNota" placeholder="Digite uma nota..." />
        <button @click="adicionarNota">Adicionar</button>
    
        <div class="notas">
            <NotaItem
                v-for="(nota, index) in notas"
                :key="index"
                :texto="nota.texto"
                :concluida="nota.concluida"
                @remover="removerNotas(index)"
                @concluir="concluirNota(index)"
                @editar="editarNota(index, $event)"
            />
        </div>
    </div>
</template>

<script>
import NotaItem from './components/Nota.vue'

export default {
    components: { NotaItem },
    data() {
        return {
            novaNota: '',
            notas: []
        }
    },
    methods: {
        adicionarNota() {
            if (this.novaNota.trim() !== '') {
                this.notas.push({
                    texto: this.novaNota.trim(),
                    concluida: false
                })
                this.novaNota = ''
            }
        },
        removerNotas(index) {
            this.notas.splice(index, 1)
        },
        concluirNota(index) {
            this.notas[index].concluida = !this.notas[index].concluida
        },
        editarNota(index, novoTexto) {
            this.notas[index].texto = novoTexto
        }
    }
}
</script>

<style>
body {
    background-color: #fdf6e3;
    font-family: 'Arial', sans-serif;
}

.container {
    background-color: #fff8dc;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0,0,0,0.05);
}

input {
    width: 100%;
    padding: 10px;
    margin-bottom: 10px;
}

button {
    background-color: #87cefa;
    color: white;
    border: none;
    padding: 10px 20px;
    cursor: pointer;
}

.notas {
    display: flex;
    flex-direction: column;
    gap: 10px;
}
</style>

        