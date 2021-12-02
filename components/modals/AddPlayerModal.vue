<template>
    <div>
        <b-button variant="primary" v-b-modal.add-player-modal>
            <BIconPersonPlus /> Crear jugador
        </b-button>
        <b-modal id="add-player-modal" title="Creando nuevo jugador" @show="resetModal" @hidden="resetModal" @ok="handleOk">
            <form ref="form" @submit.stop.prevent="handleSubmit">
                <b-form-group invalid-feedback="Nombre obligatorio" :state="nameState">
                    <b-form-input placeholder="Nombre *" id="name-input" v-model="name" :state="nameState" required></b-form-input>
                </b-form-group>

                <b-form-input v-model="lastName" placeholder="Apellido"></b-form-input>

                <b-form-group invalid-feedback="Posición obligatoria" :state="positionState">
                    <b-form-select v-model="position" :options="positions" class="mt-3" required></b-form-select>
                </b-form-group>

                <b-form-group invalid-feedback="Nivel obligatorio" :state="levelState">
                    <b-form-select v-model="level" :options="levels" class="mt-1" required></b-form-select>
                </b-form-group>
            </form>
        </b-modal>
    </div>
</template>

<script lang="ts">
import Vue from 'vue';
import { BIconPersonPlus } from 'bootstrap-vue';

export default Vue.extend({
    components: { BIconPersonPlus },
    data() {
        return {
            name: '',
            nameState: <any> null,
            lastName: '',
            position: null,
            positionState: <any> null,
            positions: [
              { value: null, text: 'Selecciona una posición *' },
              { value: 'SIN PREFERENCIA', text: 'SIN PREFERENCIA' },
              { value: 'REVÉS', text: 'REVÉS' },
              { value: 'DERECHA', text: 'DERECHA' }
            ],
            level: null,
            levelState: <any> null,
            levels: [
                { value: null, text: 'Selecciona un nivel *' },
                { value: 1, text: '1ª - PRIMERA' },
                { value: 2, text: '2ª - SEGUNDA' },
                { value: 3, text: '3ª - TERCERA' },
                { value: 4, text: '4ª - CUARTA' },
                { value: 5, text: '5ª - QUINTA' }
            ]
        }
    },
    methods: {
      checkFormValidity() {
        const valid = (this.$refs.form as Vue & { checkValidity: () => boolean }).checkValidity();
        this.nameState = this.name ? true : false;
        this.positionState = this.position ? true : false;
        this.levelState = this.level ? true : false;
        return valid;
      },
      resetModal() {
        this.name = '';
        this.nameState = null;
        this.position = null;
        this.positionState = null;
        this.level = null;
        this.levelState = null;
      },
      handleOk(bvModalEvt: any) {
        bvModalEvt.preventDefault();
        this.handleSubmit();
      },
      handleSubmit() {
        if (!this.checkFormValidity()) {
          return;
        }
        this.$nextTick(() => {
          this.$bvModal.hide('add-player-modal');
        });
      }
    }
})
</script>