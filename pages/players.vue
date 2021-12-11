<template>
    <div>
        <div class="mb-4">
            <AddPlayerModal />
        </div>

        <Table :items="items" :fields="fields"/>
    </div>
</template>

<script lang="ts">
import Vue from 'vue';
import localforage from 'localforage';
import AddPlayerModal from '~/components/modals/AddPlayerModal.vue'

export default Vue.extend({
    components: { AddPlayerModal },
    async asyncData() {
        //TODO: fix refresh page 'No available storage method found' error
        let players: any = [];
        await localforage.iterate((value, key) => {players.push(value)});
        return { items: players };
    },
    data() {
        return {
            fields: [
                { key: 'level', label: 'Nivel', sortable: true },
                { key: 'name', label: 'Nombre', sortable: true },
                { key: 'lastName', label: 'Apellido', sortable: true },
                { key: 'position', label: 'Posición', sortable: true },
                //{ key: 'bestShot', label: 'Golpe estrella', sortable: true },
            ]
        }
    }
})
</script>