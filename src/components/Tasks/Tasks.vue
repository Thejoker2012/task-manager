<template>
    <q-item
            @click="updateTask({id: id, updates: {completed: !task.completed}})"
            :class="!task.completed ? 'bg-orange-1':'bg-green-1'"
            v-touch-hold:1000.mouse="showEditTaskModal"
            clickable
            v-ripple>
        <q-item-section side top>
            <q-checkbox :value="task.completed" class="no-pointer-events"/>
        </q-item-section>

        <q-item-section>
            <q-item-label
                    :class="{'text-strikethrough' : task.completed}"
                    v-html="$options.filters.searchHighlight(task.name, search)"
            >
            </q-item-label>
        </q-item-section>

        <q-item-section side>
            <div class="row">
                <div class="column justify-center">
                    <q-icon name="event" size="18px" class="q-mr-xs"></q-icon>
                </div>
                <div class="column">
                    <q-item-label caption class="row justify-end">{{task.dueDate | niceDate}}</q-item-label>
                    <q-item-label caption class="row justify-end">
                        <small>{{task.dueTime}}</small>
                    </q-item-label>
                </div>
            </div>
        </q-item-section>

        <q-item-section side>
            <div class="row">
                <q-btn @click.stop="showEditTaskModal" flat round color="primary" icon="edit" dense></q-btn>
                <q-btn @click.stop="promptToDelete(id)" flat round color="red" icon="delete" dense></q-btn>
            </div>
        </q-item-section>


        <q-dialog v-model="showEditTask">
            <edit-task
                    @close="showEditTask=false"
                    :task="task"
                    :id="id"
            ></edit-task>
        </q-dialog>

    </q-item>
</template>

<script>
    import {mapState,mapActions} from 'vuex'
    import {date} from 'quasar'

    export default {
        props: ['task', 'id'],
        data: () => ({
            showEditTask: false
        }),
        methods: {
            ...mapActions('tasks', ['updateTask', 'deleteTask']),
            promptToDelete(id) {
                this.$q.dialog({
                    title: 'Excluir',
                    message: `Você tem certeza que quer excluir esta tarefa ?`,
                    ok: {
                        push: true
                    },
                    cancel: {
                        color: 'negative'
                    },
                    persistent: true
                }).onOk(() => {
                    this.deleteTask(id)
                })
            },
            showEditTaskModal() {
                this.showEditTask = true
            }

        },
        filters: {
            niceDate(value) {
                return date.formatDate(value, 'MMM D')
            },
            searchHighlight(value, search){
                console.log('Value', value)
                console.log('Search', search)
                if(search){
                    let searchRegExp = new RegExp(search, 'ig')
                    return value.replace(searchRegExp, (match)=>{
                        return '<span class="bg-yellow-6">'+ match +'</span>'
                    })
                }

                return value
            }
        },
        components: {
            'edit-task':
            require('./Modals/EditTask').default
        },
        computed:{
            ...mapState('tasks', ['search'])
        }
    }
</script>

<style scoped>

</style>