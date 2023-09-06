<template>
  <body>
    <div class="container">
      <LeftBox :step="step" />
      <div class="right-container" :class="{ centered: step === 5 }">
        <div v-if="step === 1">
          <PersonalInfo v-if="step === 1" :formData="formData" @updateFormData="updateFormData" />
          <div class="under-div">
            <NextBtn @goNext="nextStep" />
          </div>
          
        </div>
        <div v-if="step === 2">
          <SelectPlan :formData="formData" @updateFormData="updateFormData" />
          <div>
            <BackBtn @goBack="goBack" />
            <NextBtn @goNext="nextStep" />
          </div>
        </div>

        <div v-if="step === 3">
          <AddOns :formData="formData" @updateFormData="updateFormData" />
          <div>
            <BackBtn @goBack="goBack" />
            <NextBtn @goNext="nextStep" />
          </div>
        </div>

        <div v-if="step === 4">
          <SummaryStep :formData="formData" @changePlan="changePlan" />
          <div>
            <BackBtn @goBack="goBack" />
            <ConfirmBtn @goNext="nextStep" />
          </div>
        </div>
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
import NextBtn from './NextBtn.vue'
import BackBtn from './BackBtn.vue'
import ConfirmBtn from './ConfirmBtn.vue'
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
  components: {
    LeftBox,
    AddOns,
    PersonalInfo,
    SelectPlan,
    SummaryStep,
    ThankYou,
    NextBtn,
    BackBtn,
    ConfirmBtn
  },
  methods: {
    nextStep() {
      if (this.step < 5) {
        this.step++
      }
    },
    updateFormData(key, value) {
      this.formData[key] = value
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
  position: relative;
}
.container {
  height: 610px;
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

@media only screen and (max-width: 1000px) {
  body {
    min-height: auto;
  }
  .container {
    background-color: hsl(217, 100%, 97%);
    border: none;
    box-shadow: none;
    height: 90vh;
  }
  .right-container {
    position: initial;
    background-color: hsl(231, 100%, 99%);
    border: none;
    display: flex;
    z-index: 2;
    padding: 30px 25px;
    border-radius: 10px;
    box-shadow: 0 3px 10px rgb(0 0 0 / 0.2);
    margin: 10px 0;
    margin-top: 100px;
    width: 100%;
    height: 450px;
  }
  .under-div{
    height: 60px;
    width: 100%;
    position: absolute;
    bottom: 0;
    transform: translateY(100%);
    right: 20px;
  }
}
</style>
