<template>
  <div>
    <HeaderMain title="Select your plan"></HeaderMain>
    <ParagraphMain title="You have the option of monthly or yearly billing."></ParagraphMain>
    <form action="" @submit.prevent="next">
      <div>
        <div class="planContainer">
          <PlanStyle
            v-for="(plan, key) in plans"
            :key="key"
            :name="plan.name"
            :image="plan.image"
            :monthly-billing="plan.monthlyBilling"
            :yearly-billing="plan.yearlyBilling"
            :paidMonthly="formData.paidMonthly"
            :active="plan.name === formData.plan"
            @changeActive="updateActivePlan"
          />
          
        </div>
        <div class="switch-container">
          <p :class="{ active: formData.paidMonthly }">Monthly</p>
          <toggleSwitch :paidMonthly="formData.paidMonthly" @togglePaidMonthly="changeBilling" />
          <p :class="{ active: !formData.paidMonthly }">Yearly</p>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import HeaderMain from '../components/HeaderMain.vue'
import ParagraphMain from '../components/ParagraphMain.vue'
import PlanStyle from '../components/PlanStyle.vue'
import toggleSwitch from '../components/toggle-switch.vue'
export default {
  data() {
    return {
      plans: [
        {
          name: 'Arcade',
          image: 'arcade',
          monthlyBilling: 9,
          yearlyBilling: 90,
          active: true
        },
        {
          name: 'Advanced',
          image: 'advanced',
          monthlyBilling: 12,
          yearlyBilling: 120,
          active: false
        },
        {
          name: 'Pro',
          image: 'pro',
          monthlyBilling: 15,
          yearlyBilling: 150,
          active: false
        }
      ]
    }
  },
  props: ['formData'],
  components: { HeaderMain, ParagraphMain, PlanStyle, toggleSwitch },
  methods: {
    changeBilling() {
      const updatedPaidMonthly = !this.formData.paidMonthly
      this.$emit('updateFormData', 'paidMonthly', updatedPaidMonthly)
      if (this.formData.onlineService) {
        this.$emit('updateFormData', 'onlineServicePrice', updatedPaidMonthly ? 1 : 10)
      }

      if (this.formData.largeStorage) {
        this.$emit('updateFormData', 'largeStoragePrice', updatedPaidMonthly ? 2 : 20)
      }

      if (this.formData.customizableProfile) {
        this.$emit('updateFormData', 'customizableProfilePrice', updatedPaidMonthly ? 2 : 20)
      }
      const activePlan = this.plans.find((plan) => plan.active)
      if (activePlan) {
        const planPrice = updatedPaidMonthly ? activePlan.monthlyBilling : activePlan.yearlyBilling
        this.$emit('updateFormData', 'planPrice', planPrice)
      }
    },
    updateActivePlan(name) {
      for (let i = 0; i < this.plans.length; i++) {
        if (this.plans[i].name === name) {
          this.plans[i].active = true
          this.$emit('updateFormData', 'plan', name)
          this.$emit(
            'updateFormData',
            'planPrice',
            this.formData.paidMonthly ? this.plans[i].monthlyBilling : this.plans[i].yearlyBilling
          )
        } else {
          this.plans[i].active = false
        }
      }
    }
  }
}
</script>

<style scoped>
.planContainer {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

.active {
  transition: 0.3s;
  color: hsl(213, 96%, 18%);
}

.switch-container {
  display: flex;
  background-color: hsl(217, 100%, 97%);
  border-radius: 10px;
  justify-content: center;
  align-items: center;
  margin-top: 40px;
  font-weight: 500;
  padding: 15px 0;
}

form {
  display: flex;
  flex-direction: column;
}

@media only screen and (max-width: 1000px) {
  .planContainer {
    flex-direction: column;
  }
  .switch-container{
    margin-top: 20px;
  }
}
</style>
