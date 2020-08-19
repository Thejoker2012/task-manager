<template xmlns:v-slot="http://www.w3.org/1999/XSL/Transform">
    <div
            class="row q-mb-sm"
    >
        <q-input
                label="Hora"
                outlined
                class="col"
                :value="dueTime"
                @input="$emit('update:dueTime', $event)"
                :rules="[val => !!val || 'Campo obrigatório!']"
        >
            <template v-slot:append>
                <q-icon
                        v-if="dueTime"
                        @click="$emit('update:dueTime', '')"
                        name="close"
                        class="cursor-pointer"
                ></q-icon>
                <q-icon name="access_time" class="cursor-pointer">
                    <q-popup-proxy transition-show="scale" transition-hide="scale">
                        <q-time :value="dueTime" @input="$emit('update:dueTime', $event)"
                        ></q-time>
                    </q-popup-proxy>
                </q-icon>
            </template>
        </q-input>
    </div>
</template>

<script>
    export default {
        name: "ModalDueTime",
        props:['dueTime']
    }
</script>

<style scoped>

</style>