<template>
  <body>
    <div class="container">
      <LeftBox :step="step" />
      <div class="right-container" :class="{ centered: step === 5 }">
        <transition name="fade" mode="out-in">
          <component
            :is="currentStepComponent"
            :formData="formData"
            @updateFormData="updateFormData"
            @changePlan="changePlan"
            :key="step"
          />
        </transition>
        <div class="under-div under-full-size">
          <NextBtn v-if="step <= 3" @goNext="nextStep" />
          <ConfirmBtn v-if="step === 4" @goNext="nextStep" />
          <BackBtn v-if="step >= 2 && step <= 4" @goBack="goBack" />
        </div>
      </div>
      <div class="under-div" :class="{ 'under-small-size': step >= 1 && step <= 4 }">
        <NextBtn v-if="step <= 3" @goNext="nextStep" />
        <ConfirmBtn v-if="step === 4" @goNext="nextStep" />
        <BackBtn v-if="step >= 2 && step <= 4" @goBack="goBack" />
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
        isValid: false,
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
  computed: {
    currentStepComponent() {
      switch (this.step) {
        case 1:
          return PersonalInfo
        case 2:
          return SelectPlan
        case 3:
          return AddOns
        case 4:
          return SummaryStep
        case 5:
          return ThankYou
        default:
          return null
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
      if (this.step === 1) {
        this.formData.isValid = true
        if (this.validatePersonalInfo()) {
          this.step++
        }
      } else if (this.step < 5) {
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
    },
    validatePersonalInfo() {
      const isValidName = this.formData.name.trim() !== ''
      const emailPattern = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}$/
      const isValidEmail =
        this.formData.email.trim() !== '' && emailPattern.test(this.formData.email)
      const phonePattern = /^\+\d{12}$/
      const isValidPhone =
        this.formData.phone.trim() !== '' && phonePattern.test(this.formData.phone)

      this.nameError = !isValidName
      this.emailError = !isValidEmail ? 'Invalid email format' : ''
      this.phoneError = !isValidPhone ? 'Invalid phone number format' : ''

      return isValidName && isValidEmail && isValidPhone
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

.under-small-size {
  display: none;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

@media only screen and (max-width: 1000px) {
  body {
    min-height: auto;
  }
  .container {
    background-color: hsl(217, 100%, 97%);
    box-shadow: none;
    height: 90vh;
  }

  .right-container {
    position: absolute;
    background-color: hsl(231, 100%, 99%);
    z-index: 2;
    padding: 30px 25px;
    border-radius: 10px;
    box-shadow: 0 3px 10px rgb(0 0 0 / 0.2);
    margin-top: 100px;
    margin-left: auto;
    margin-right: auto;
    left: 0;
    right: 0;
  }
  .under-div {
    height: 60px;
    position: absolute;
    bottom: 0;
    transform: translateY(100%);
    left: 20px;
    right: 20px;
  }

  .under-full-size {
    display: none;
  }

  .under-small-size {
    display: block;
  }
}

@media only screen and (max-width: 500px) {
  .right-container {
    width: 90vw;
  }
}

@media only screen and (max-width: 400px) {
  .right-container {
    width: 90vw;
    margin-top: 50px;
  }
  body {
    min-height: 100vh;
  }
}
</style>
