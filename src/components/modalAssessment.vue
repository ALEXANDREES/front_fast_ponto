<template>
  <q-dialog persistent v-model="openModalAssessment">
    <q-card style="width: 300px">
      <div class="row justify-center q-py-md q-px-sm">
        <span class="col-12 text-center text-bold text-grey-8"> Por favor avalie a plataforma </span>
        <q-form @submit.prevent="onSubmit()" class="q-mt-lg">
          <q-rating
            v-model="assessment"
            max="5"
            size="3.5em"
            color="primary"
            icon="star_border"
            icon-selected="star"
            no-dimming
          />

          <div class="q-mt-lg row justify-center">
            <q-btn no-caps label="Concluir" type="submit" color="primary"/>
          </div>
        </q-form>
      </div>
    </q-card>
  </q-dialog>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'modalAssessment',
  setup() {
    return {
      openModalAssessment: ref(false),
      assessment: ref(1),
      user: ({})
    }
  },
  props: {
    userData: Object
  },
  methods: {
    open() {
      this.openModalAssessment = true
    },
    onSubmit() {
      this.user = this.userData
      this.user.assessment = this.assessment

      console.log(this.user)

      this.$q.notify({
        position: "bottom",
        color: "primary",
        textColor: "white",
        icon: "check",
        message: 'Formulário preenchido com sucesso!',
      })

      this.openModalAssessment = false

      this.$router.replace({ name: 'registerSuccess' })
    }
  }
}
</script>

