<template>
  <div>
    <img src="/images/icon-thank-you.svg">
    <HeaderMain title="Thank you!"></HeaderMain>
    <ParagraphMain class="summary-paragraph" title="Thanks for confirming your subscription! We hope you have fun using our platform. If you ever need support, please feel free to email us at support@loremgaming.com."></ParagraphMain>
  </div>
</template>

<script>

import HeaderMain from '../components/HeaderMain.vue'
import ParagraphMain from '../components/ParagraphMain.vue'
export default {
  components: { HeaderMain, ParagraphMain }
}
</script>

<style scoped>
div {
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: center;
}

img {
  margin-bottom: 30px;
}

.summary-paragraph {
  max-width: 450px;
  align-items: center;
  display: flex;
  line-height: 24px;
  text-align: center;
}

</style>
