<template xmlns:v-slot="http://www.w3.org/1999/XSL/Transform">
    <div
            class="row q-mb-sm"
    >
        <q-input
                label="Data"
                outlined
                :value="dueDate"
                :ref="dueDate "
                class="col"
                @input="$emit('update:dueDate', $event)"
                :rules="[val => !!val || 'Campo obrigatório!']"
        >
            <template v-slot:append>
                <q-icon
                        v-if="dueDate"
                        @click="$emit('clear')"
                        name="close"
                        class="cursor-pointer"
                ></q-icon>
                <q-icon name="event" class="cursor-pointer">
                    <q-popup-proxy>
                        <q-date :value="dueDate" @input="$emit('update:dueDate', $event)"></q-date>
                    </q-popup-proxy>
                </q-icon>
            </template>
        </q-input>
    </div>
</template>

<script>
    export default {
        name: "ModelDueDate",
        props: ['dueDate'],
        methods: {

            clearDueDate() {
                this.taskToSubmit.dueDate = ''
                this.taskToSubmit.dueTime = ''
            }
        }
    }
</script>

<style scoped>

</style>