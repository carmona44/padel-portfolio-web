<template>
    <div>
        <b-navbar>
            <b-button variant="outline-primary" v-b-toggle.sidebar-menu>
                <BIconList aria-label="Show Sidebar" />
            </b-button>
        </b-navbar>
    </div>
</template>

<script lang="ts">
import Vue from 'vue';
import { BIconList } from 'bootstrap-vue';

export default Vue.extend({
    components: { BIconList, }
})
</script>
