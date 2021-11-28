<template>
    <div>
        <b-button variant="outline-primary" class="ml-4 mt-4" v-b-toggle.sidebar-1>
            <BIconList icon="list" aria-label="Show Sidebar" />
        </b-button>
        <b-sidebar id="sidebar-1" title="Pádel Portfolio" shadow backdrop>
            <div class="px-3 py-2"></div>
        </b-sidebar>
    </div>
</template>

<script lang="ts">
import Vue from 'vue';
import { BIconList } from 'bootstrap-vue';

export default Vue.extend({
    components: { BIconList }
})
</script>