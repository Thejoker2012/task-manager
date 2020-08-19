<template xmlns:v-slot="http://www.w3.org/1999/XSL/Transform">
  <div class="row q-mb-sm">
    <q-input
      outlined
      :value="name"
      @input="$emit('update:name', $event)"
      label="Tarefa"
      class="col"
      autofocus
      v-select-all
      ref="name"
      :rules="[val => !!val || 'Campo obrigatório!']"
    >
      <template v-slot:append>
        <q-icon
          v-if="name"
          @click="$emit('update:name', '')"
          name="close"
          class="cursor-pointer"
        ></q-icon>
      </template>
    </q-input>
  </div>
</template>

<script>
import { selectAll } from "src/directives/directive-select-all";

export default {
  name: "ModalTaskName",
  props: ["name"],
  directives: {
    selectAll
  }
};
</script>

<style scoped></style>
