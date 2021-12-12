<template>
    <div>
        <b-button variant="primary" v-b-modal.add-player-modal>
            <BIconPersonPlus /> Crear jugador
        </b-button>
        <b-modal id="add-player-modal" title="Creando nuevo jugador" @show="resetModal" @hidden="resetModal" @ok="handleOk">
            <form ref="form" @submit.stop.prevent="handleSubmit">
                <b-form-group invalid-feedback="Nombre obligatorio" :state="nameState">
                    <b-form-input placeholder="Nombre *" id="name-input" v-model="player.name" :state="nameState" required></b-form-input>
                </b-form-group>

                <b-form-group invalid-feedback="Posición obligatoria" :state="positionState">
                    <b-form-select v-model="player.position" :options="positions" class="mt-1" required></b-form-select>
                </b-form-group>

                <b-form-group invalid-feedback="Nivel obligatorio" :state="levelState">
                    <b-form-select v-model="player.level" :options="levels" class="mt-1" required></b-form-select>
                </b-form-group>

                <b-form-group invalid-feedback="Mano dominante obligatoria" :state="dominantHandState">
                    <b-form-select v-model="player.dominantHand" :options="dominantHand" class="mt-1" required></b-form-select>
                </b-form-group>

                <b-form-group invalid-feedback="Mejor golpe obligatorio" :state="bestShotState">
                    <b-form-select v-model="player.bestShot" :options="shots" class="mt-1" required></b-form-select>
                </b-form-group>
            </form>
        </b-modal>
    </div>
</template>

<script lang="ts">
import Vue from 'vue';
import localforage from 'localforage';
import { BIconPersonPlus } from 'bootstrap-vue';
import { POSITIONS, LEVELS, DOMINANT_HAND, SHOTS } from '@/utils/constants/player';

export default Vue.extend({
    components: { BIconPersonPlus },
    data() {
        return {
            player: { 
              name: '',
              position: null,
              level: null,
              dominantHand: null,
              bestShot: null
            },
            nameState: <any> null,
            positionState: <any> null,
            positions: POSITIONS,
            levelState: <any> null,
            levels: LEVELS,
            dominantHandState: <any> null,
            dominantHand: DOMINANT_HAND,
            bestShotState: <any> null,
            shots: SHOTS
        }
    },
    methods: {
      checkFormValidity() {
        const valid = (this.$refs.form as Vue & { checkValidity: () => boolean }).checkValidity();
        this.nameState = this.player.name ? true : false;
        this.positionState = this.player.position ? true : false;
        this.levelState = this.player.level ? true : false;
        this.dominantHandState = this.player.dominantHand ? true : false;
        this.bestShotState = this.player.bestShot ? true : false;
        return valid;
      },
      resetModal() {
        this.player = { 
          name: '',
          position: null,
          level: null,
          dominantHand: null,
          bestShot: null
        };
        this.nameState = null;
        this.positionState = null;
        this.levelState = null;
        this.dominantHandState = null;
        this.bestShotState = null;
      },
      handleOk(bvModalEvt: any) {
        bvModalEvt.preventDefault();
        this.handleSubmit();
      },
      async handleSubmit() {
        if (!this.checkFormValidity()) {
          return;
        }
        await localforage.setItem(`${new Date().getTime()}`, this.player);
        this.$nextTick(() => {
          this.$bvModal.hide('add-player-modal');
        });
      }
    }
})
</script>