<template>
   <li class="list-group-item">
    <span>{{contato.nome}} : {{contato.id}}</span>
    <router-link
     :to="{ path: `/contatos/${contato.id}` }"
     class="btn btn-info btn-sm float-right">
     Detalhes
     </router-link>
     <!---<button
        class="btn btn-info btn-sm float-right"
        @click="verDetalhes">Detalhes</button>--->
    </li>
</template>
<script>
export default {
    props:{
        contato: {
            type: Object,
            required: true
        }
    },
    methods: {
       /* verDetalhes(){
            //this.$router.push(`/contatos/${this.contato.id}`)
            //this.$router.push({ path: `/contatos/${this.contato.id}` })
            this.$router.push({ name: 'contato', params: { id: this.contato.id } })
        }*/
    },
}
</script>
