<template>
    <Table :items="items" :fields="fields"/>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
    data() {
        return {
            items: [
                { name: 'Daniel', lastName: 'Carmona', position: 'Left', level: 4, bestShot: 'Volea' },
                { name: 'David', lastName: 'Navarro', position: 'Right', level: 4, bestShot: 'Globo' },
                { name: 'David', lastName: 'Alemán', position: 'Right', level: 4, bestShot: 'Smash' },
                { name: 'Antonio', lastName: 'Macdonald', position: 'Left', level: 4, bestShot: 'Dejada' },
            ],
            fields: [
                { key: 'level', label: 'Nivel', sortable: true },
                { key: 'name', label: 'Nombre', sortable: true },
                { key: 'lastName', label: 'Apellido', sortable: true },
                { key: 'position', label: 'Posición', sortable: true },
                { key: 'bestShot', label: 'Golpe estrella', sortable: true },
            ]
        }
    }
})
</script>