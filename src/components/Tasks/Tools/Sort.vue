<template>
    <q-select
            class="col q-ml-sm"
            filled
            v-model="sortBy"
            emit-value
            map-options
            :options="options"
            label="OrderBy"
            stack-label></q-select>
</template>

<script>
    import {mapState, mapActions} from 'vuex'

    export default {
        name: "Sort",
        data: () => ({
            options: [
                {
                    label: 'Name',
                    value: 'name'
                },
                {
                    label: 'Date',
                    value: 'dueDate'
                },
            ],

            dense: false,
            denseOpts: false
        }),
        methods:{
          ...mapActions('tasks', ['setSort'])
        },
        computed: {
            ...mapState('tasks', ['sort']),
            sortBy: {
                get() {
                    return this.sort
                },
                set(value) {
                    this.setSort(value)
                }
            }
        }
    }
</script>

<style scoped>
    .q-select {
        flex: 0 0 112px;
    }
</style>