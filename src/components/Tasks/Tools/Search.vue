<template xmlns:v-slot="http://www.w3.org/1999/XSL/Transform">
    <q-input
            outlined
            class="col"
            v-model="searchField"
            label="Search"
            @keyup.esc="searchField = ''"
    >
        <template v-slot:append>
            <q-icon v-if="searchField !== ''" name="close" @click="searchField = ''" class="cursor-pointer" />
            <q-icon name="search" />
        </template>

    </q-input>
</template>

<script>
    import {mapState, mapActions} from 'vuex'
    import {selectAll} from 'src/directives/directive-select-all'

    export default {
        name: "Search",
        computed:{
            ...mapState(['search']),
            searchField:{
               get(){
                   return this.search
               },
                set(value){
                   this.setSearch(value)
                }
            }
        },
        methods:{
            ...mapActions('tasks',['setSearch'])
        },
        directives: {
            selectAll
        }
    }
</script>

<style scoped>

</style>