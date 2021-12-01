<template>
    <div>
        <div class="mb-4">
            <b-button variant="primary" @click="modalShow = !modalShow">
                <BIconPersonPlus /> Crear jugador
            </b-button>

            <AddPlayerModal :modalShow="modalShow"/>
        </div>

        <Table :items="items" :fields="fields"/>
    </div>
</template>

<script lang="ts">
import Vue from 'vue';
import { BIconPersonPlus } from 'bootstrap-vue';
import AddPlayerModal from '~/components/modals/AddPlayerModal.vue'

export default Vue.extend({
    components: { BIconPersonPlus, AddPlayerModal },
    data() {
        return {
            modalShow: false,
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