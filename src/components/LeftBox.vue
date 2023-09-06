<template>
  <div class="containerOne">
    <ul>
      <li>
        <div class="number" :class="{ active: stepNumber === 0 }">1</div>
        <div class="step"><span>STEP 1</span>YOUR INFO</div>
      </li>
      <li>
        <div class="number" :class="{ active: stepNumber === 1 }">2</div>
        <div class="step"><span>STEP 2</span>SELECT PLAN</div>
      </li>
      <li>
        <div class="number" :class="{ active: stepNumber === 2 }">3</div>
        <div class="step"><span>STEP 3</span>ADD-ONS</div>
      </li>
      <li>
        <div class="number" :class="{ active: stepNumber === 3 }">4</div>
        <div class="step"><span>STEP 4</span>SUMMARY</div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'LeftBox',
  props: {
    step: {
      Number
    }
  },
  computed: {
    stepNumber() {
      switch (this.step) {
        case 1:
          return 0
        case 2:
          return 1
        case 3:
          return 2
        case 4:
          return 3
        case 5:
          return 3
        default:
          return 0
      }
    }
  }
}
</script>

<style scoped>
.containerOne {
  color: hsl(0, 0%, 100%);
  background-image: url('./images/bg-sidebar-desktop.svg');
  width: 274px;
  padding: 30px;
  background-repeat: no-repeat;
}

ul {
  display: flex;
  flex-direction: column;
}
li {
  display: flex;
  overflow: hidden;
  margin-bottom: 30px;
}

.step {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-left: 10px;
  letter-spacing: 0.5px;
  font-weight: 500;
}

.step span {
  font-size: 14px;
  color: hsl(231, 11%, 63%);
}
.number {
  border: 2px solid hsl(0, 0%, 100%);
  padding: 8px 12px;
  border-radius: 50%;
  font-weight: 500;
}
.active {
  background-color: hsl(206, 94%, 87%);
  border-color: hsl(206, 94%, 87%);
  color: black;
}

@media only screen and (max-width: 1000px) {
  .containerOne {
    position: absolute;
    top: 0;
    left:0;
    z-index: 1;
    height: 240px;
    width: 100%;
    background-position: center bottom 10% ;
    background-size: 100%;
    border-radius: none;
  }
  ul {
    justify-content: space-evenly;
    flex-direction: row;
  }
  .step {
    display: none;
  }
}
</style>
