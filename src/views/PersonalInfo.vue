<template>
  <div class="personal-info">
    <HeaderMain title="Personal info"></HeaderMain>
    <ParagraphMain
      title="Please provide your name, email address, and phone number."
    ></ParagraphMain>
    <form action="" @submit.prevent="submitForm">
      <div class="flex-end">
        <label for="name">Name</label>
        <div class="error" v-if="nameError && nameBlurred">This Field is required</div>
      </div>
      <input
        type="text"
        placeholder="e.g. Stephen King"
        :value="formData.name"
        @input="$emit('updateFormData', 'name', $event.target.value)"
        @blur="checkNameInput"
        @focus="nameBlurred = false"
        :class="{ 'error-border': nameError }"
      />
      <div class="flex-end">
        <label for="name">Email Address</label>
        <div class="error" v-if="emailError && emailBlurred">{{ emailError }}</div>
      </div>
      <input
        type="email"
        placeholder="e.g. stephenking@lorem.com"
        :value="formData.email"
        @input="$emit('updateFormData', 'email', $event.target.value)"
        @blur="checkEmailInput"
        @focus="emailBlurred = false"
        :class="{ 'error-border': emailError }"
      />
      <div class="flex-end">
        <label for="name">Phone Number</label>
        <div class="error" v-if="phoneError && phoneBlurred">{{ phoneError }}</div>
      </div>

      <input
        type="tel"
        placeholder="e.g. +1 234 567 890"
        :value="formData.phone"
        @input="$emit('updateFormData', 'phone', $event.target.value)"
        @blur="checkPhoneInput"
        @focus="phoneBlurred = false"
        :class="{ 'error-border': phoneError }"
      />
    </form>
  </div>
</template>

<script>
import HeaderMain from '../components/HeaderMain.vue'
import ParagraphMain from '../components/ParagraphMain.vue'
export default {
  components: { HeaderMain, ParagraphMain },
  props: ['formData'],
  data() {
    return {
      nameError: false,
      emailError: '',
      phoneError: '',
      nameBlurred: false,
      emailBlurred: false,
      phoneBlurred: false
    }
  },

  methods: {
    checkNameInput() {
      this.nameError = !this.formData.name.trim()
      this.nameBlurred = true
    },
    checkEmailInput() {
      const emailPattern = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}$/
      if (!this.formData.email.trim()) {
        this.emailError = 'This field is required'
        this.emailBlurred = true
      } else if (!emailPattern.test(this.formData.email)) {
        this.emailError = 'Invalid email format'
        this.emailBlurred = true
      } else {
        this.emailError = ''
      }
    },
    checkPhoneInput() {
      const phonePattern = /^\+\d{12}$/
      if (!this.formData.phone.trim()) {
        this.phoneError = 'This field is required'
        this.phoneBlurred = true
      } else if (!phonePattern.test(this.formData.phone)) {
        this.phoneError = 'Invalid phone number format'
        this.phoneBlurred = true
      } else {
        this.phoneError = ''
      }
    }
  }
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

.error {
  color: red;
}

.error-border {
  border-color: red;
}
</style>
