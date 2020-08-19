<template>
    <q-banner
            dense
            inline-actions
            class=" list-header text-white text-center shadow-2"
            :class="bgcolor"
    >
        <strong class="text-bold text-subtitle1"><slot></slot></strong>
    </q-banner>
</template>

<script>
    export default {
        name: "ListHeader",
        props:['bgcolor']
    }
</script>

<style scoped>
.list-header{
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
}
</style>