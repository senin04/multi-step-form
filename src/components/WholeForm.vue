<template>
  <body>
    <div class="Container">
      <LeftBox :step="step" />
      <div class="right-container" :class="{ centered: step === 5 }">
        <PersonalInfo
          @next="nextStep"
          v-if="step === 1"
          :formData="formData"
          @updateFormData="updateFormData"
        />
        <SelectPlan
          @next="nextStep"
          @goBack="goBack"
          v-if="step === 2"
          :formData="formData"
          @updateFormData="updateFormData"
        />
        <AddOns
          @next="nextStep"
          @goBack="goBack"
          v-if="step === 3"
          :formData="formData"
          @updateFormData="updateFormData"
        />
        <SummaryStep
          v-if="step === 4"
          @next="nextStep"
          @goBack="goBack"
          :formData="formData"
          @changePlan="changePlan"
        />
        <ThankYou v-if="step === 5" />
      </div>
    </div>
  </body>
</template>

<script>
import LeftBox from './LeftBox.vue'
import AddOns from '../views/AddOns.vue'
import PersonalInfo from '../views/PersonalInfo.vue'
import SelectPlan from '../views/SelectPlan.vue'
import SummaryStep from '../views/SummaryStep.vue'
import ThankYou from '../views/ThankYou.vue'
export default {
  data() {
    return {
      step: 1,
      formData: {
        name: '',
        email: '',
        phone: '',
        plan: 'Arcade',
        paidMonthly: true,
        planPrice: 9,
        onlineService: true,
        onlineServicePrice: 1,
        largeStorage: true,
        largeStoragePrice: 2,
        customizableProfile: false,
        customizableProfilePrice: 0
      }
    }
  },
  components: { LeftBox, AddOns, PersonalInfo, SelectPlan, SummaryStep, ThankYou },
  methods: {
    nextStep() {
      if (this.step < 5) {
        this.step++
      }
    },
    updateFormData(key, value) {
      this.formData[key] = value;
      // console.log( this.formData.planPrice)
    },
    goBack() {
      this.step--
    },
    changePlan() {
      this.step = 2
    }
  }
}
</script>

<style scoped>
body {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: hsl(217, 100%, 97%);
}
.Container {
  height: 608px;
  padding: 20px;
  background-color: hsl(231, 100%, 99%);
  border-radius: 10px;
  display: flex;
  box-shadow: 0 3px 10px rgb(0 0 0 / 0.2);
}

.right-container {
  position: relative;
  margin: 0 90px;
  width: 460px;
  margin-top: 40px;
  margin: 40px 90px 20px 90px;
  display: flex;
  justify-content: space-between;
  flex-direction: column;
}

.right-container.centered {
  justify-content: center;
}
</style>
