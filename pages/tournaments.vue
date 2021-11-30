<template>
    <Table :items="items"/>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
    data() {
        return {
            items: [
                { name: 'Padelnuestro', city: 'Murcia', format: 'League', prueba: true },
                { name: 'Villaescusa', city: 'Alicante', format: 'KO', prueba: false },
                { name: 'Padel Murcia', city: 'Murcia', format: 'KO', prueba: false },
                { name: 'WPT', city: 'Madrid', format: 'KO', prueba: true },
            ]
        }
    }
})
</script>