<template>
   <div>
    <div class="row">
        <div class="col-sm-10">
            <h1 class="font-weight-light">Lista de Tarefas</h1>
        </div>
        <div class="col-sm-2">
            <button class="btn btn-primary float-right" @click="exibirFormularioCriarTarefa">
                <i class="bi bi-plus mr-2"></i>
                <span>Criar</span>
            </button>
        </div>
    </div>
    <br>

    <h3 class="font-weight-light">A Fazer:  {{ totaldeTarefasAFazer }}</h3>
    <ul class="list-group" v-if="tarefasAFazer.length > 0">
        <tarefa-lista-iten v-for="tarefa in tarefasAFazer" :key="tarefa.id" :tarefa="tarefa" @concluir="concluirTarefa({tarefa: $event})" @editar="selecionarTarefaParaEdicao"></tarefa-lista-iten>
    </ul>

    <p v-else>Nenhuma tarefa a fazer.</p>
    <br>

    <h3 class="font-weight-light">Concluidas:  {{ totaldeTarefasConcluidas }}</h3>
    <ul class="list-group" v-if="tarefasConcluidas.length > 0">
        <tarefa-lista-iten v-for="tarefa in tarefasConcluidas" :key="tarefa.id" :tarefa="tarefa" @concluir="concluirTarefa({tarefa: $event})" @editar="selecionarTarefaParaEdicao"></tarefa-lista-iten>
    </ul>
    <p v-else>Nenhuma tarefa concluida.</p>

    <tarefa-salvar
     v-if="exibirFormulario" 
     @criar="criarTarefa"
     @editar="editarTarefa"
     :tarefa="tarefaSelecionada" />
    </div>
</template>

<script>
import { createNamespacedHelpers } from 'vuex'
//import axios from 'axios'

import TarefaListaIten from './TarefaListaIten.vue'
import TarefaSalvar from './TarefaSalvar.vue'
//import register from './../_store/register'
//import config from '../../config/config'

const { mapActions, mapGetters, mapState } = createNamespacedHelpers('tarefas')

export default {
    components: {
        TarefaListaIten,
        TarefaSalvar
    },
    computed: {
        ...mapState(['tarefas']),
        ...mapGetters(['tarefasConcluidas', 'tarefasAFazer', 'totaldeTarefasConcluidas', 'totaldeTarefasAFazer', 'boasVindas']),
        /*tarefasConcluidas(){
            return this.$store.getters.tarefasConcluidas;
        },
        tarefasAFazer(){
            return this.$store.getters.tarefasAFazer;
        }*/
    },
    data(){
        return{
            exibirFormulario: false,
            tarefaSelecionada: undefined
        }
    },
 //   created(){
     // axios.get(`${config.apiURL}/tarefas`)
     // .then((response) => {
     //   this.tarefas = response.data;
     // })
   // },
    methods: {
        //...mapMutations(['listarTarefas']),
        /*...mapMutations({
            //carregarTarefas: 'listarTarefas'
            carregarTarefas: (commit, payload, options) => {
                commit('listarTarefas', payload, options)
            }
        }),
        ...mapActions({
            carregarTarefas: 'listarTarefas',
            listarTarefas: (dispatch, payload, options) => {
                return dispatch('listarTarefas', payload, options)
            },
            
        }),*/
        ...mapActions([
            'concluirTarefa',
            'listarTarefas'
        ]),
        exibirFormularioCriarTarefa(){
            if(this.tarefaSelecionada){
                this.tarefaSelecionada = undefined;
                return
            }
            this.exibirFormulario = !this.exibirFormulario;
        },
        /*criarTarefa(tarefa){
            console.log('Criar: ', tarefa);
            this.$store.state.tarefas.push(tarefa);
            this.resetar();                
        },
        editarTarefa(tarefa){
                console.log('Editar: ', tarefa);
                const indice = this.$store.state.tarefas.findIndex(t => t.id === tarefa.id);
                this.$store.state.tarefas.splice(indice, 1, tarefa);
                this.resetar();
        },*/
        resetar(){
            this.exibirFormulario = false,
            this.tarefaSelecionada = undefined
        },
        selecionarTarefaParaEdicao(tarefa){
             this.tarefaSelecionada = tarefa;
             this.exibirFormulario = true;
        }
    },
    created(){
        //this.$store.commit('listarTarefas');
            //this.carregarTarefas();
            /*setTimeout(async () => {
            await this.$store.dispatch({
                type: 'listarTarefas',
                tarefas: [
                {id: 1, titulo: 'Aprender Vue', concluido: true},
                {id: 2, titulo: 'Aprender JS', concluido: true},
                {id: 3, titulo: 'Aprender Axios', concluido: false},    
            ]
            });
            }, 3000)
            this.$store.commit('listarTarefas').then(() => {
                console.log('Actions executadas');
            })
            setTimeout(async () => {
                console.log('Usuario atual: ', this.boasVindas);
                await this.listarTarefas()
                console.log('Actions executadas');
            }, 3000)
            console.log('Boas vindas: ', this.boasVindas)*/
            //register(this.$store);
            this.listarTarefas();
    }
}
</script>