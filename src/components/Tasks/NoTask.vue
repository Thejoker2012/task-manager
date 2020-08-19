<template xmlns:v-slot="http://www.w3.org/1999/XSL/Transform">
    <q-banner class="bg-grey-3">
        <template v-slot:avatar>
            <q-icon name="check" color="primary" />
        </template>
        Nenhuma tarefa programada para hoje!
        <template v-slot:action>
            <q-btn
                    flat
                    color="primary"
                    label="Adicionar Tarefa"
                    @click="$emit('showAddTask')"
            ></q-btn>
        </template>
    </q-banner>
</template>

<script>
    export default {
        name: "NoTask"
    }
</script>

<style scoped>

</style>