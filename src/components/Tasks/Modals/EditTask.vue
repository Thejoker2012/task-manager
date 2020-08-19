<template xmlns:v-slot="http://www.w3.org/1999/XSL/Transform">
    <q-card class="modal-widht">

        <modal-header>Editar Tarefa</modal-header>

        <q-form @submit.prevent="submitForm">
            <q-card-section class="q-pt-none">

                <modal-task-name
                        :name.sync="taskToSubmit.name"
                ></modal-task-name>

                <modal-due-date
                        v-show="taskToSubmit.name"
                        :dueDate.sync="taskToSubmit.dueDate"
                        @clear="clearDueDate"
                ></modal-due-date>

                <modal-due-time
                        v-show="taskToSubmit.dueDate"
                        :dueTime.sync="taskToSubmit.dueTime"
                ></modal-due-time>

            </q-card-section>

            <q-card-actions align="right">

                <modal-buttom></modal-buttom>

            </q-card-actions>

        </q-form>

    </q-card>
</template>

<script>
    import {mapActions} from 'vuex'

    export default {
        name: "EditTask",
        props: ['id', 'task'],
        data: () => ({
            taskToSubmit: {}
        }),
        methods: {
            ...mapActions('tasks', ['updateTask']),
            submitForm() {
                this.updateTask(
                    {
                        id: this.id,
                        updates: this.taskToSubmit
                    }
                )
                this.$emit('close')
            },
            clearDueDate() {
                this.taskToSubmit.dueDate = ''
                this.taskToSubmit.dueTime = ''
            }
        },
        components: {
            'modal-header': require('./Shared/ModalHeader').default,
            'modal-task-name': require('./Shared/ModalTaskName').default,
            'modal-due-date': require('./Shared/ModelDueDate').default,
            'modal-due-time': require('./Shared/ModalDueTime').default,
            'modal-buttom': require('./Shared/ModalButton').default
        },
        mounted() {
            this.taskToSubmit = Object.assign({}, this.task)
        }
    }
</script>

<style scoped>

    .modal-widht{
        width: 600px;
    }

</style>