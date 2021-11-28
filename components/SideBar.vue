<template>
    <div>
        <b-button variant="outline-primary" class="ml-4 mt-4" v-b-toggle.sidebar-1>
            <BIconList icon="list" aria-label="Show Sidebar" />
        </b-button>
        <b-sidebar id="sidebar-1" title="Pádel Portfolio" shadow backdrop>
            <b-nav vertical>
                <b-nav-item><NuxtLink to="/stats"><BIconPieChart aria-label="Go to stats page"/> Stats</NuxtLink></b-nav-item>
                <b-nav-item><NuxtLink to="/players"><BIconPeople aria-label="Go to players page"/> Jugadores</NuxtLink></b-nav-item>
                <b-nav-item><NuxtLink to="/matches"><BIconIntersect aria-label="Go to matches page"/> Partidos</NuxtLink></b-nav-item>
                <b-nav-item><NuxtLink to="/clubs"><BIconHouseDoor aria-label="Go to clubs page"/> Clubes</NuxtLink></b-nav-item>
                <b-nav-item><NuxtLink to="/tournaments"><BIconTrophy aria-label="Go to tournaments page"/> Torneos</NuxtLink></b-nav-item>
            </b-nav>
            <template #footer>
                <div align="center" class="mb-3">
                    <div>
                        Made with <NuxtLogo/>, <a href="https://bootstrap-vue.org/"><BIconBootstrap /></a> and ❤️
                    </div>
                    <div class="mt-2">
                        By 
                        <a href="https://github.com/carmona44">
                            <b-img height="20" src="../static/dc-favicon.png"></b-img>
                        </a>
                    </div>
                </div>
            </template>
        </b-sidebar>
    </div>
</template>

<script lang="ts">
import Vue from 'vue';
import { BIconList, BIconPieChart, BIconPeople, BIconHouseDoor, 
    BIconTrophy, BIconIntersect, BIconBootstrap } from 'bootstrap-vue';

export default Vue.extend({
    components: { 
        BIconList, BIconPieChart, BIconPeople, BIconHouseDoor, BIconTrophy, BIconIntersect, BIconBootstrap 
    }
})
</script>