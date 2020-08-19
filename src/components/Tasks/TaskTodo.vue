<template>
    <div>

        <list-header :bgcolor="'bg-orange-4'">Tarefas</list-header>

        <q-list

                separator
                bordered
        >
            <task
                    v-for="(task, index) in tasksTodo"
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
        props: ['tasksTodo'],
        components: {
            'task': require('./Tasks').default,
            'list-header': require('./../Shared/ListHeader').default,
        }
    }
</script>

<style scoped>

</style>