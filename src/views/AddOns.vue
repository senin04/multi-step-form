<template>
  <div>
    <HeaderMain title="Pick add-ons"></HeaderMain>
    <ParagraphMain title="Add-ons help enchance your gaming experience."></ParagraphMain>
    <form action="" @submit.prevent="next">
      <div class="addonContainer">
        <AddonsStyle
          v-for="(addon, key) in addons"
          :key="key"
          :name="addon.name"
          :yearlyBilling="addon.yearlyBilling"
          :monthlyBilling="addon.monthlyBilling"
          :text="addon.text"
          :active="addon.active"
          :id="addon.id"
          :paidMonthly="formData.paidMonthly"
          @changeActive="updateActive"
        />
      </div>
      <!-- <BackBtn @goBack="goBack" />
      <NextBtn /> -->
    </form>
  </div>
</template>

<script>
// import NextBtn from '../components/NextBtn.vue'
import HeaderMain from '../components/HeaderMain.vue'
import ParagraphMain from '../components/ParagraphMain.vue'
// import BackBtn from '../components/BackBtn.vue'
import AddonsStyle from '../components/AddonsStyle.vue'
export default {
  data() {
    return {
      addons: [
        {
          id: 1,
          value: 'onlineService',
          name: 'Online service',
          text: 'Access to multiplayer games',
          monthlyBilling: 1,
          yearlyBilling: 10,
          active: this.formData.onlineService
        },
        {
          id: 2,
          value: 'largeStorage',
          name: 'Large storage',
          text: 'Extra 1TB of cloud save',
          monthlyBilling: 2,
          yearlyBilling: 20,
          active: this.formData.largeStorage
        },
        {
          id: 3,
          value: 'customizableProfile',
          name: 'Customizable profile',
          text: 'Custom theme on your profile',
          monthlyBilling: 2,
          yearlyBilling: 20,
          active: this.formData.customizableProfile
        }
      ]
    }
  },
  components: {  HeaderMain, ParagraphMain, AddonsStyle },
  props: ['formData'],
  methods: {
    // next() {
    //   this.$emit('next')
    // },
    // goBack() {
    //   this.$emit('goBack')
    // },
    updateActive(name) {
      for (let i = 0; i < this.addons.length; i++) {
        if (this.addons[i].name === name) {
          this.addons[i].active = !this.addons[i].active
          this.$emit('updateFormData', this.addons[i].value, this.addons[i].active)
          if (this.addons[i].active === true) {
            this.$emit('updateFormData', this.addons[i].value+ 'Price', this.formData.paidMonthly ? this.addons[i].monthlyBilling : this.addons[i].yearlyBilling )
          } else {
            this.$emit('updateFormData', this.addons[i].value+ 'Price', 0)
          }
          
        }
      }
    }
  }
}
</script>

<style scoped>
.addonContainer {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

form {
  display: flex;
  flex-direction: column;
}
</style>
