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
            positions: [
              { value: null, text: 'Selecciona una posición *' },
              { value: 'SIN PREFERENCIA', text: 'SIN PREFERENCIA' },
              { value: 'REVÉS', text: 'REVÉS' },
              { value: 'DERECHA', text: 'DERECHA' }
            ],
            levelState: <any> null,
            levels: [
                { value: null, text: 'Selecciona un nivel *' },
                { value: 1, text: '1ª - PRIMERA' },
                { value: 2, text: '2ª - SEGUNDA' },
                { value: 3, text: '3ª - TERCERA' },
                { value: 4, text: '4ª - CUARTA' },
                { value: 5, text: '5ª - QUINTA' }
            ],
            dominantHandState: <any> null,
            dominantHand: [
                { value: null, text: 'Selecciona mano dominante *' },
                { value: 'AMBIDIESTRO', text: 'AMBIDIESTRO' },
                { value: 'DIESTRO', text: 'DIESTRO' },
                { value: 'ZURDO', text: 'ZURDO' },
            ],
            bestShotState: <any> null,
            shots: [
                { value: null, text: 'Selecciona su mejor golpe *' },
                { value: 'VOLEA DERECHA', text: 'VOLEA DERECHA' },
                { value: 'VOLEA REVÉS', text: 'VOLEA REVÉS' },
                { value: 'BANDEJA', text: 'BANDEJA' },
                { value: 'REMATE PLANO', text: 'REMATE PLANO' },
                { value: 'REMATE LIFTADO', text: 'REMATE LIFTADO' },
                { value: 'GLOBO', text: 'GLOBO' },
                { value: 'DEJADA', text: 'DEJADA' },
                { value: 'SAQUE', text: 'SAQUE' },
                { value: 'DERECHA', text: 'DERECHA' },
                { value: 'REVÉS', text: 'REVÉS' },
                { value: 'RULO A LA REJA', text: 'RULO A LA REJA' },
                { value: 'VÍBORA', text: 'VÍBORA' },
                { value: 'CHIQUITA', text: 'CHIQUITA' },
            ]
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