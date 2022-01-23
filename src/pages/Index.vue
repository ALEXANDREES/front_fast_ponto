<template>
  <div>
    <q-form class="row justify-center text-center items-center q-mt-lg" @submit.prevent="onSubmit">
      <div class="textSubtitleStepper text-h6 col-12 q-mb-xl">
        Passo {{ currentStepper }} de 4
      </div>

      <div class="col-xl-1 col-lg-1 col-md-2 col-sm-2 col-xs-2">
        <q-avatar disable class="shadow-6" round size="65px" :color="checkSelectedAvatarForColorPersonalData()">
          <template v-slot>
            <q-img class="iconsAvatarsSteps" :src="checkSelectedAvatarForImagePersonalData()" />
          </template>
        </q-avatar>
        <span class="gt-xs textSubtitleStepper row justify-center col-12 q-mt-md"> Dados Pessoais </span>
      </div>
      <q-separator class="gt-xs col-1 q-mb-xl q-mt-md bg-primary" style="height: 2px;"/>
      <q-separator class="lt-sm col-1 q-mb-md q-mt-md bg-primary" style="height: 2px;"/>

      <div class="col-xl-1 col-lg-1 col-md-2 col-sm-2 col-xs-2">
        <q-avatar class="shadow-6" round size="65px" :color="checkSelectedAvatarForColorSignatories()">
          <template v-slot>
            <q-img class="iconsAvatarsSteps" :src="checkSelectedAvatarForImageSignatories()" />
          </template>
        </q-avatar>
        <span class="gt-xs textSubtitleStepper row justify-center col-12 q-mt-md"> Endereço </span>
      </div>
      <q-separator class="gt-xs col-1 q-mb-xl q-mt-md bg-primary" style="height: 2px;"/>
      <q-separator class="lt-sm col-1 q-mb-md q-mt-md bg-primary" style="height: 2px;"/>

      <div class="col-xl-1 col-lg-1 col-md-2 col-sm-2 col-xs-2">
        <q-avatar class="shadow-6" round size="65px" :color="checkSelectedAvatarForColorConfiguration()">
          <template v-slot>
            <q-img class="iconsAvatarsSteps" :src="checkSelectedAvatarForImageConfiguration()" />
          </template>
        </q-avatar>
        <span class="gt-xs textSubtitleStepper row justify-center col-12 q-mt-md"> Preferência Musical </span>
      </div>
      <q-separator class="gt-xs col-1 q-mb-xl q-mt-md bg-primary" style="height: 2px;"/>
      <q-separator class="lt-sm col-1 q-mb-md q-mt-md bg-primary" style="height: 2px;"/>

      <div class="col-xl-1 col-lg-1 col-md-2 col-sm-2 col-xs-2">
        <q-avatar class="shadow-6" round size="65px" :color="checkSelectedAvatarForColorSend()">
          <template v-slot>
            <q-img class="iconsAvatarsSteps" :src="checkSelectedAvatarForImageSend()" />
          </template>
        </q-avatar>
        <span class="gt-xs textSubtitleStepper row justify-center col-12 q-mt-md"> Sistema </span>
      </div>

      <div
        class="row col-xl-6 col-lg-6 col-md-6 col-sm-6 col-xs-11 justify-center q-mt-xl q-py-md shadow-3"
        style="border: 1px solid #00afef; border-radius: 5px;"
        v-if="selectedAvatarPersonalData && displayAvatarPersonalData"
      >
        <div class="row col-11 justify-center">
          <span class="col-11 text-left textSubtitleStepper text-subtitle1"> Nome: </span>
          <q-input
            class="col-11"
            input-class="text-secondary"
            color="primary"
            dense
            outlined
            v-model="user.name"
          />
        </div>

        <div class="row col-11 justify-center">
          <span class="col-11 text-left textSubtitleStepper text-subtitle1"> Sobrenome: </span>
          <q-input
            class="col-11"
            input-class="text-secondary"
            color="primary"
            dense
            outlined
            v-model="user.lastName"
          />
        </div>
      </div>

      <div
        class="row col-xl-6 col-lg-6 col-md-6 col-sm-6 col-xs-11 justify-center q-mt-xl q-py-md shadow-3"
        style="border: 1px solid #00afef; border-radius: 5px;"
        v-if="selectedAvatarAddress && displayAvatarAddress"
      >
        <div class="row col-11 justify-center">
          <span class="col-11 text-left textSubtitleStepper text-subtitle1"> País: </span>
          <q-select
            class="col-11"
            input-class="text-secondary"
            color="primary"
            dense
            outlined
            option-label="nome"
            :options="listCountrys"
            v-model="user.country"
          />
        </div>

        <div class="row col-11 justify-center">
          <span class="col-11 text-left textSubtitleStepper text-subtitle1"> CEP: </span>
          <q-input
            class="col-11"
            input-class="text-secondary"
            color="primary"
            dense
            outlined
            v-model="user.cep"
            mask="##.###-###"
            unmasked-value
            @blur="searchCityByCep()"
          />
        </div>

        <div class="row col-11 justify-center">
          <span class="col-11 text-left textSubtitleStepper text-subtitle1"> Endereço: </span>
          <q-input
            class="col-11"
            input-class="text-secondary"
            color="primary"
            dense
            outlined
            v-model="user.address"
          />
        </div>

        <div class="row col-11 justify-center">
          <span class="col-11 text-left textSubtitleStepper text-subtitle1"> Número: </span>
          <q-input
            class="col-11"
            input-class="text-secondary"
            color="primary"
            dense
            outlined
            v-model="user.number"
            type="number"
          />
        </div>

        <div class="row col-11 justify-center">
          <span class="col-11 text-left textSubtitleStepper text-subtitle1"> Cidade: </span>
          <q-input
            class="col-11"
            input-class="text-secondary"
            color="primary"
            dense
            outlined
            v-model="user.city"
            readonly
          />
        </div>
      </div>

      <div
        class="row col-xl-6 col-lg-6 col-md-6 col-sm-6 col-xs-11 justify-center q-mt-xl q-py-md shadow-3"
        style="border: 1px solid #00afef; border-radius: 5px;"
        v-if="selectedAvatarMusicalPreference && displayAvatarMusicalPreference"
      >
        <div class="row col-11 justify-center">
          <span class="col-11 text-left textSubtitleStepper text-subtitle1"> Estilos Musicais: </span>
          <q-option-group
            class="col-11 text-left"
            :options="optionsMusicalPreference"
            type="checkbox"
            v-model="user.musicalPreference"
          />
        </div>
      </div>

      <div
        class="row col-xl-6 col-lg-6 col-md-6 col-sm-6 col-xs-11 justify-center q-mt-xl q-py-md shadow-3"
        style="border: 1px solid #00afef; border-radius: 5px;"
        v-if="selectedAvatarOperationalSystem && displayAvatarOperationalSystem"
      >
        <div class="row col-11 justify-center">
          <span class="col-11 text-left textSubtitleStepper text-subtitle1"> Sistema: </span>
          <q-radio
            class="col-11"
            name="shape"
            v-model="user.operationalSystem"
            val="windows"
            label="Windows"
          />
          <q-radio
            class="col-11"
            name="shape"
            v-model="user.operationalSystem"
            val="linux"
            label="Linux"
          />
          <q-radio
            class="col-11"
            name="shape"
            v-model="user.operationalSystem"
            val="macOs"
            label="MacOS"
          />
        </div>
      </div>

      <div class="row col-12 justify-evenly q-mt-md">
        <q-btn
          class="bg-primary text-white text-bold"
          label="Voltar"
          no-caps
          dense
          flat
          :disable="currentStepper === 1"
          @click="nextOrPreviousStepper('anterior')"
        />

        <q-btn
          class="bg-primary text-white text-bold"
          :label="currentStepper === 4 ? 'Finalizar' : 'Próximo'"
          no-caps
          dense
          flat
          type="submit"
          @click="currentStepper === 4 ? nextOrPreviousStepper('finalizar') : nextOrPreviousStepper('proximo') "
        />
      </div>
    </q-form>

    <modal-assessment :userData="user" ref="modalAssessment"/>
  </div>
</template>

<script>
import { ref } from 'vue'
import axios from 'axios'
import f from '../functions/util'
import modalAssessment from 'src/components/modalAssessment.vue'

export default {
  components: {
    modalAssessment
  },
  name: 'PageIndex',
  setup () {
    return {
      currentStepper: ref(1),
      selectedAvatarPersonalData: ref(true),
      selectedAvatarAddress: ref(false),
      selectedAvatarMusicalPreference: ref(false),
      selectedAvatarOperationalSystem: ref(false),
      displayAvatarPersonalData: ref(true),
      displayAvatarAddress: ref(false),
      displayAvatarMusicalPreference: ref(false),
      displayAvatarOperationalSystem: ref(false),
      user: ref({
        name: '',
        lastName: '',
        country: '',
        cep: '',
        address: '',
        number: '',
        city: '',
        musicalPreference: [],
        operationalSystem: '',
        assessment: false
      }),
      listCountrys: ref([]),
      optionsMusicalPreference: [
        {
          label: "Rock",
          value: "rock"
        },
        {
          label: "Reggae",
          value: "reggae"
        },
        {
          label: "Sertanejo",
          value: "sertanejo"
        },
        { label: "Funk",
          value: "funk"
        },
        {
          label: "Axé",
          value: "axe"
        },
        {
          label: "Samba",
          value: "samba"
        }
      ],
      messageError: ref('')
    }
  },
  mounted() {
    this.listCountrys = f().countryList()
  },
  methods: {
    currentStep() {
      if (this.currentStepper === 1) {
        this.selectedAvatarPersonalData = true
        this.selectedAvatarAddress = false
        this.selectedAvatarMusicalPreference = false
        this.selectedAvatarOperationalSystem = false

        this.displayAvatarPersonalData = true
        this.displayAvatarAddress = false
        this.displayAvatarMusicalPreference = false
        this.displayAvatarOperationalSystem = false
      } else if (this.currentStepper === 2) {
        this.selectedAvatarPersonalData = true
        this.selectedAvatarAddress = true
        this.selectedAvatarMusicalPreference = false
        this.selectedAvatarOperationalSystem = false

        this.displayAvatarPersonalData = false
        this.displayAvatarAddress = true
        this.displayAvatarMusicalPreference = false
        this.displayAvatarOperationalSystem = false
      } else if (this.currentStepper === 3) {
        this.selectedAvatarPersonalData = true
        this.selectedAvatarAddress = true
        this.selectedAvatarMusicalPreference = true
        this.selectedAvatarOperationalSystem = false

        this.displayAvatarPersonalData = false
        this.displayAvatarAddress = false
        this.displayAvatarMusicalPreference = true
        this.displayAvatarOperationalSystem = false
      } else if (this.currentStepper === 4) {
        this.selectedAvatarPersonalData = true
        this.selectedAvatarAddress = true
        this.selectedAvatarMusicalPreference = true
        this.selectedAvatarOperationalSystem = true

        this.displayAvatarPersonalData = false
        this.displayAvatarAddress = false
        this.displayAvatarMusicalPreference = false
        this.displayAvatarOperationalSystem = true
      }
    },
    checkSelectedAvatarForColorPersonalData() {
      if (this.selectedAvatarPersonalData) {
        return 'primary'
      } else {
        return 'white'
      }
    },
    checkSelectedAvatarForImagePersonalData() {
      if (this.selectedAvatarPersonalData) {
        return '/icons/personal_data_white.svg'
      } else {
        return '/icons/personal_data_primary.svg'
      }
    },
    checkSelectedAvatarForColorSignatories() {
      if (this.selectedAvatarAddress) {
        return 'primary'
      } else {
        return 'white'
      }
    },
    checkSelectedAvatarForImageSignatories() {
      if (this.selectedAvatarAddress) {
        return '/icons/location_white.svg'
      } else {
        return '/icons/location_primary.svg'
      }
    },
    checkSelectedAvatarForColorConfiguration() {
      if (this.selectedAvatarMusicalPreference) {
        return 'primary'
      } else {
        return 'white'
      }
    },
    checkSelectedAvatarForImageConfiguration() {
      if (this.selectedAvatarMusicalPreference) {
        return '/icons/musical_preference_white.svg'
      } else {
        return '/icons/musical_preference_primary.svg'
      }
    },
    checkSelectedAvatarForColorSend() {
      if (this.selectedAvatarOperationalSystem) {
        return 'primary'
      } else {
        return 'white'
      }
    },
    checkSelectedAvatarForImageSend() {
      if (this.selectedAvatarOperationalSystem) {
        return '/icons/operational_system_white.svg'
      } else {
        return '/icons/operational_system_primary.svg'
      }
    },
    nextOrPreviousStepper(type) {
      switch (this.currentStepper) {
        case 1:
          this.checkFieldsPersonalData(type)
        break

        case 2:
          this.checkFieldsAddress(type)
        break

        case 3:
          this.checkFieldsMusicalPreference(type)
        break

        case 4:
          this.checkFieldsOperationalSystem(type)
        break

        default:
          this.messageError = 'O stepper fornecido não existe!'
          this.messageErrorContent()
        break
      }
    },
    checkFieldsPersonalData(type) {
      if (type === 'proximo') {
        if (this.user.name === '' || this.user.lastName === '') {
          this.messageError = 'Os campos nome e sobrenome devem ser preenchidos!'
          return this.messageErrorContent()
        } else {
          this.currentStepper += 1
          this.currentStep()
        }
      } else if (type === 'anterior') {
          this.currentStepper -= 1
          this.currentStep()
      }
    },
    checkFieldsAddress(type) {
      if (type === 'proximo') {
        if (this.user.country === '' || this.user.cep === '' || this.user.address === '' || this.user.number === '' || this.user.city === '') {
          this.messageError = 'Os campos país, cep, endereço, número e cidade devem ser preenchidos!'

          if (this.user.cep.length < 8) {
            this.messageError = 'O campo CEP deve conter oito caracteres!'
          }

          return this.messageErrorContent()
        } else {
          this.currentStepper += 1
          this.currentStep()
        }
      } else if (type === 'anterior') {
          this.currentStepper -= 1
          this.currentStep()
      }
    },
    checkFieldsMusicalPreference(type) {
      if (type === 'proximo') {
        if (this.user.musicalPreference && this.user.musicalPreference.length === 0) {
          this.messageError = 'O campo preferência musical deve ser preenchido!'
          return this.messageErrorContent()
        } else {
          this.currentStepper += 1
          this.currentStep()
        }
      } else if (type === 'anterior') {
          this.currentStepper -= 1
          this.currentStep()
      }
    },
    checkFieldsOperationalSystem(type) {
      if (type === 'proximo') {
        if (this.user.operationalSystem === '') {
          this.messageError = 'O campo sistema operacional deve ser preenchido!'
          return this.messageErrorContent()
        } else {
          this.currentStepper += 1
          this.currentStep()
        }
      } else if (type === 'anterior') {
        this.currentStepper -= 1
        this.currentStep()
      } else if (type === 'finalizar') {
        if (this.user.operationalSystem === '') {
          this.messageError = 'O campo sistema operacional deve ser preenchido!'
          return this.messageErrorContent()
        } else {
          this.user.assessment = true
        }
      }
    },
    searchCityByCep() {
      if (this.user.cep !== '' && this.user.cep.length === 8) {
        axios.get('https://viacep.com.br/ws/'+this.user.cep+'/json/').then((res) => {
          this.user.city = res.data.localidade
        })
      }
    },
    messageErrorContent() {
      this.$q.notify({
        position: "bottom",
        color: "negative",
        textColor: "white",
        icon: "error",
        message: this.messageError,
      })
    },
    onSubmit() {
      if (this.user.name !== '' && this.user.lastName !== '' && this.user.country !== '' && this.user.cep !== '' && this.user.address !== '' && this.user.number !== '' && this.user.city !== '' && this.user.musicalPreference.length > 0 && this.user.operationalSystem !== '') {
        if (this.user.assessment) {
          setTimeout(() => { this.$refs.modalAssessment.open() }, 250)
        }
      }
    }
  }
}
</script>

<style scoped>
.iconsAvatarsSteps {
  width: 40px;
  height: 40px;
}
.textSubtitleStepper {
  color: #808080;
  font-weight: bold;
}
</style>
