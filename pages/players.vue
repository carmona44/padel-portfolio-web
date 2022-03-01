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
        try {
            let players: any = [];
            await localforage.iterate((value, key) => {players.push(value)});
            return { items: players };
        } catch (error) {
            console.log(error);
        }
    },
    data() {
        return {
            fields: [
                { key: 'level', label: 'Nivel', sortable: true },
                { key: 'name', label: 'Nombre', sortable: true },
                { key: 'position', label: 'Posición', sortable: true },
                { key: 'dominantHand', label: 'Mano dominante', sortable: true },
                { key: 'bestShot', label: 'Mejor golpe', sortable: true },
            ]
        }
    }
})
</script>