<template>
  <div>
    <HeaderMain title="Finishing up"></HeaderMain>
    <ParagraphMain title="Double-check everything looks OK before confirming."></ParagraphMain>
    <form action="" @submit.prevent="next">
      <div class="container">
        <div class="small-container">
          <div>
            <div class="bold-text">
              {{ formData.plan }} {{ formData.paidMonthly ? '(Monthly)' : '(Yearly)' }}
            </div>
            <a @click.prevent="changePlan" href="">Change</a>
          </div>
          <div class="bold-text">
            ${{ formData.planPrice }}{{ formData.paidMonthly ? '/mo' : '/yr' }}
          </div>
        </div>
        <p v-if="formData.onlineService">
          Online service
          <span>+${{ formData.onlineServicePrice }}{{ formData.paidMonthly ? '/mo' : '/yr' }}</span>
        </p>
        <p v-if="formData.largeStorage">
          Larger storage<span
            >+${{ formData.largeStoragePrice }}{{ formData.paidMonthly ? '/mo' : '/yr' }}</span
          >
        </p>
        <p v-if="formData.customizableProfile">
          Customizable profile<span
            >+${{ formData.customizableProfilePrice
            }}{{ formData.paidMonthly ? '/mo' : '/yr' }}</span
          >
        </p>
        
      </div>
      <p class="total">Total(per year)<span
            >${{ countPrice()
            }}{{ formData.paidMonthly ? '/mo' : '/yr' }}</span
          ></p>
      <BackBtn @goBack="goBack" />
      <ConfirmBtn/>
    </form>
  </div>
</template>

<script>
import HeaderMain from '../components/HeaderMain.vue'
import ParagraphMain from '../components/ParagraphMain.vue'
import BackBtn from '../components/BackBtn.vue'
import ConfirmBtn from '../components/ConfirmBtn.vue'
export default {
  data() {
    return {}
  },
  components: { HeaderMain, ParagraphMain, BackBtn, ConfirmBtn },
  props: ['formData'],
  methods: {
    next() {
      this.$emit('next')
    },
    goBack() {
      this.$emit('goBack')
    },
    updateActive(name) {
      for (let i = 0; i < this.addons.length; i++) {
        if (this.addons[i].name === name) {
          this.addons[i].active = !this.addons[i].active
        }
      }
    },
    changePlan() {
      this.$emit('changePlan')
    },
    countPrice() {
      // console.log(this.formData.planPrice , this.formData.onlineServicePrice , this.formData.largeStoragePrice, this.formData.customizableProfilePrice)
      return this.formData.planPrice + this.formData.onlineServicePrice + this.formData.largeStoragePrice+ this.formData.customizableProfilePrice
    }
  }
}
</script>

<style scoped>
.container {
  background-color: hsl(217, 100%, 97%);
  padding: 30px;
}

form {
  display: flex;
  flex-direction: column;
}

.small-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding-bottom: 20px;
  border-bottom: 0.2px solid hsl(220, 4%, 86%);
  margin-bottom: 20px;
}

.bold-text {
  color: hsl(213, 96%, 18%);
  font-size: 16px;
  font-weight: 500;
  margin-bottom: 6px;
}

a {
  color: hsl(231, 11%, 63%);
  transition: 0.2s;
  text-decoration-thickness: 2px;
}

a:hover {
  color: hsl(243, 100%, 62%);
}

p {
  display: flex;
  justify-content: space-between;
  margin-top: 20px;
}

span {
  color: hsl(213, 96%, 18%);
}

.total {
  padding: 10px 30px;
}
.total span {
  font-weight: 700;
  font-size: 20px;
  color: hsl(243, 100%, 62%);
}
</style>
