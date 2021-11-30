<template>
    <div>
        <b-table 
            responsive 
            striped 
            hover 
            sort-icon-left
            :items="items" 
            :fields="fields"
        ></b-table>
    </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
    props: ['items', 'fields']
})
</script>