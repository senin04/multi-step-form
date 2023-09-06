<template>
  <div class="personal-info">
    <HeaderMain title="Personal info"></HeaderMain>
    <ParagraphMain
      title="Please provide your name, email address, and phone number."
    ></ParagraphMain>
    <form action="" @submit.prevent="next">
      <div class="flex-end">
        <label for="name">Name</label>
        <!-- <div class="error">This Field is required</div> -->
      </div>
      <input
        type="text"
        placeholder="e.g. Stephen King"
        :value="formData.name"
        @input="$emit('updateFormData', 'name', $event.target.value)"
      />
      <label for="name">Email Address</label>
      <!-- <span class="error">This Field is required</span> -->
      <input
        type="email"
        placeholder="e.g. stephenking@lorem.com"
        :value="formData.email"
        @input="$emit('updateFormData', 'email', $event.target.value)"
      />
      <label for="name">Phone Number</label>
      <input
        type="tel"
        placeholder="e.g. +1 234 567 890"
        :value="formData.phone"
        @input="$emit('updateFormData', 'phone', $event.target.value)"
      />
      <!-- <NextBtn /> -->
    </form>
  </div>
</template>

<script>
// import NextBtn from '../components/NextBtn.vue'
import HeaderMain from '../components/HeaderMain.vue'
import ParagraphMain from '../components/ParagraphMain.vue'
export default {
  components: {  HeaderMain, ParagraphMain },
  props: ['formData'],
  // methods: {
  //   next() {
  //     this.$emit('next')
  //   }
  // }
}
</script>

<style scoped>
.personal-info {
  position: relative;
  z-index: 2;
}
form {
  display: flex;
  flex-direction: column;
}

label {
  color: hsl(213, 96%, 18%);
  margin-bottom: 5px;
}

input {
  outline: none;
  font-size: 17px;
  font-weight: 500;
  color: hsl(213, 96%, 18%);
  padding: 15px;
  border-radius: 10px;
  border: 1px solid hsl(229, 24%, 87%);
  margin-bottom: 25px;
}

input:focus {
  border-color: hsl(243, 100%, 62%);
}

.flex-end {
  display: flex;
  justify-content: space-between;
}
</style>
