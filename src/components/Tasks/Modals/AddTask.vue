<template xmlns:v-slot="http://www.w3.org/1999/XSL/Transform">
    <q-card class="modal-widht">

        <modal-header>Adicionar Tarefa</modal-header>

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
        name: "AddTask",
        data: () => ({
            taskToSubmit: {
                name: '',
                dueDate: '',
                dueTime: '',
                completed: false,
            }
        }),
        methods: {
            ...mapActions('tasks', ['addTask']),
            submitForm() {
                this.addTask(this.taskToSubmit)
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
        }
    }
</script>

<style scoped>
    .modal-widht{
        width: 500px;
    }

</style>