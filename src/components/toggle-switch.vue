<template>
  <label class="switch">
    <input type="checkbox" :checked="!paidMonthly" @change="togglePaidMonthly"/>
    <span class="slider"></span>
  </label>
</template>

<script>
export default {
  props: ["paidMonthly"],
  methods: {
    togglePaidMonthly() {
      this.$emit('togglePaidMonthly')
    }
  }
  
}
</script>

<style scoped>
.switch {
  position: relative;
  display: inline-block;
  width: 38px;
  height: 20px;
  margin: 0 25px;
}

.switch input {
  display: none;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: hsl(213, 96%, 18%);
  -webkit-transition: 0.4s;
  transition: 0.4s;
  border-radius: 34px;
}

.slider:before {
  position: absolute;
  content: '';
  height: 13px;
  width: 13px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: 0.4s;
  transition: 0.4s;
  border-radius: 50%;
}

input:checked + .slider:before {
  -webkit-transform: translateX(17px);
  -ms-transform: translateX(17px);
  transform: translateX(17px);
}
</style>
