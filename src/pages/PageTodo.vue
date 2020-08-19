<template>
    <q-page class="q-pa-md">
        <div>

            <div class="row q-mb-lg">
                <search/>
                <sort/>
            </div>

            <p v-show="search && !Object.keys(tasksTodo).length && !Object.keys(tasksCompleted).length">Nenhuma tarefa encontrada!</p>

            <no-tasks
                    v-show="!Object.keys(tasksTodo).length && !search"
                    @showAddTask="showAddTask=true"
            />

            <tasks-todo
                    v-show="Object.keys(tasksTodo).length"
                    :tasksTodo="tasksTodo"
            />

            <tasks-completed
                    v-show="Object.keys(tasksCompleted).length"
                    :tasksCompleted="tasksCompleted"
            />

            <div class=" fixed-bottom text-center q-mb-lg botton-index botton-negative">
                <q-btn @click="showAddTask=true" round color="primary" size="24px" icon="add"
                       class="shadow-12"/>
            </div>
        </div>

        <q-dialog v-model="showAddTask">
            <add-task @close="showAddTask=false"></add-task>
        </q-dialog>
    </q-page>
</template>

<script>
    import {mapGetters, mapState} from 'vuex'

    export default {
        name: 'PageIndex',
        data: () => ({
            showAddTask: false
        }),
        components: {
            'add-task': require('../components/Tasks/Modals/AddTask').default,
            'tasks-todo': require('../components/Tasks/TaskTodo').default,
            'tasks-completed': require('../components/Tasks/TaskCompleted').default,
            'no-tasks': require('../components/Tasks/NoTask').default,
            'search': require('../components/Tasks/Tools/Search').default,
            'sort': require('../components/Tasks/Tools/Sort').default
        },
        computed: {
            ...mapGetters('tasks', ['tasksTodo', 'tasksCompleted']),
            ...mapState('tasks', ['search'])
        }
    }
</script>

<style>

    .botton-index {
        z-index: 11;
        height: 10px;
    }

    .botton-negative {
        margin-bottom: 95px;
    }

</style>
