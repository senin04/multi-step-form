<template>
  <p>
    {{ title }}
  </p>
</template>

<script>
export default {
  props: ['title']
}
</script>

<style scoped>
p {
  margin-top: 15px;
  margin-bottom: 40px;
}

@media only screen and (max-width: 1000px) {
  p {
    font-size: 18px;
}
}
</style>
