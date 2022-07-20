<script setup lang="ts">
    import { createRouter, createWebHistory } from 'vue-router'
    import NavBarComponent from "../components/NavBarComponent.vue";
    import TableComponent from "../components/TableComponent.vue";
</script>

<template>
    <NavBarComponent />
    <TableComponent :title="name"/>

</template>

<style>

</style>

<script lang="ts">
export default {
        data() {
        return {
            name: "Veronica"
        }
    }
}
</script>
<!---->