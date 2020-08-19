<template>
    <div class="q-mt-lg">

        <list-header
                :bgcolor="'bg-green-4'"
        >Tarefas concluidas</list-header>

        <q-list
                separator
                bordered
        >
            <task
                    v-for="(task, index) in tasksCompleted"
                    :key="index"
                    :task="task"
                    :id="index"

            ></task>
        </q-list>
    </div>
</template>

<script>
    export default {
        name: "TaskTodo",
        props: ['tasksCompleted'],
        components: {
            'task': require('./Tasks').default,
            'list-header': require('../Shared/ListHeader').default
        }
    }
</script>

<style scoped>

</style>