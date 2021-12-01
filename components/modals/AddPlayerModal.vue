<template>
    <b-modal id="add-player-modal" v-model="modalShow" title="Creando nuevo jugador" 
        @show="resetModal" @hidden="resetModal" @ok="handleOk">
        <form ref="form" @submit.stop.prevent="handleSubmit">
            <b-form-group label="Name" label-for="name-input" invalid-feedback="Name is required" :state="nameState">
                <b-form-input id="name-input" v-model="name" :state="nameState" required></b-form-input>
            </b-form-group>
        </form>
    </b-modal>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
    props: ['modalShow'],
    data() {
        return {
            submittedNames: new Array<string>(),
            name: '',
            nameState: <any> null
        }
    },
    methods: {
      checkFormValidity() {
        const valid = (this.$refs.form as Vue & { checkValidity: () => boolean }).checkValidity()
        this.nameState = valid
        return valid
      },
      resetModal() {
        this.name = ''
        this.nameState = null
      },
      handleOk(bvModalEvt: any) {
        // Prevent modal from closing
        bvModalEvt.preventDefault()
        // Trigger submit handler
        this.handleSubmit()
      },
      handleSubmit() {
        // Exit when the form isn't valid
        if (!this.checkFormValidity()) {
          return
        }
        // Push the name to submitted names
        this.submittedNames.push(this.name)
        // Hide the modal manually
        this.$nextTick(() => {
          this.$bvModal.hide('add-player-modal')
        })
        console.log(this.submittedNames);        
      }
    }
})
</script>