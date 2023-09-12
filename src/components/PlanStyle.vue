<template>
  <div @click="changeActive" class="box" :class="{ choosen: active }">
    <img :src="`images/icon-${image}.svg`" />
    <div class="text-container">
      <div class="bold-text">{{ name }}</div>
      <p v-if="paidMonthly">${{ monthlyBilling }}/mo</p>
      <div v-if="!paidMonthly">
        <p>${{ yearlyBilling }}/yr</p>
        <div class="free-months">2 months free</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  emits: ['changeActive'],
  props: ['image', 'name', 'monthlyBilling', 'yearlyBilling', 'enabled', 'active', 'paidMonthly'],
  methods: {
    changeActive() {
      this.$emit('changeActive', this.name)
    }
  }
}
</script>

<style scoped>
.box {
  border: 1px solid hsl(229, 24%, 87%);
  padding: 10px;
  width: 140px;
  border-radius: 10px;
  padding: 15px;
  cursor: pointer;
  transition: 0.2s;
}

.box:hover {
  border: 1px solid hsl(243, 100%, 62%);
}

.bold-text {
  color: hsl(213, 96%, 18%);
  margin-top: 40px;
  font-size: 17px;
  font-weight: 500;
  margin-bottom: 6px;
}

.free-months {
  margin-top: 6px;
  font-size: 13px;
  color: hsl(213, 96%, 18%);
  font-weight: 700;
}

.box.choosen {
  border: 1px solid hsl(243, 100%, 62%);
  background-color: hsl(217, 100%, 97%);
}

@media only screen and (max-width: 1000px) {
  .box {
    display: flex;
    flex-direction: row;
    width: 100%;
    margin-bottom: 15px;
  }
  .text-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    margin-left: 15px;
  }

  .bold-text {
    margin-top: 0;
  }
}
</style>
