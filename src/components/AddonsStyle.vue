<template>
  <input type="checkbox" :name="id" :id="id" :checked="active" @click="changeActive" />
  <label :for="id">
    <div class="box" :class="{ choosen: active }">
      <div class="small-container">
        <img src="images/icon-checkmark.svg" :class="{ choosen: active }" />
        <div>
          <div class="bold-text">{{ name }}</div>
          <p>{{ text }}</p>
        </div>
      </div>
      <p v-if="paidMonthly" class="styled-billing">+${{ monthlyBilling }}/mo</p>
      <p v-if="!paidMonthly" class="styled-billing">+${{ yearlyBilling }}/yr</p>
    </div>
  </label>
</template>

<script>
export default {
  emits: ['changeActive'],
  props: ['name', 'yearlyBilling', 'monthlyBilling', 'active', 'text', 'id', 'paidMonthly'],
  methods: {
    changeActive() {
      this.$emit('changeActive', this.name)
    }
  }
}
</script>

<style scoped>
input {
  display: none;
}
.box {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 1px solid hsl(229, 24%, 87%);
  padding: 10px;
  border-radius: 10px;
  padding: 20px;
  cursor: pointer;
  transition: 0.2s;
  margin-bottom: 20px;
}

.small-container {
  display: flex;
  align-items: center;
}

img {
  border-radius: 5px;
  height: 20px;
  padding: 5px 4px;
  margin-right: 30px;
  border: 1px solid hsl(229, 24%, 87%);
  transition: 0.3s;
}
.box:hover {
  border: 1px solid hsl(243, 100%, 62%);
}

.bold-text {
  color: hsl(213, 96%, 18%);
  font-size: 16px;
  font-weight: 700;
  margin-bottom: 6px;
}

.box.choosen {
  border: 1px solid hsl(243, 100%, 62%);
  background-color: hsl(217, 100%, 97%);
}

img.choosen {
  background-color: hsl(243, 100%, 62%);
}

p {
  font-size: 14px;
}

.styled-billing {
  font-weight: 500;
  color: hsl(243, 100%, 62%);
}
</style>
