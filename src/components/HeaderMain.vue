<template>
  <h1>{{title}}</h1>
</template>

<script>
export default {
  props: ['title']
}
</script>

<style scoped>
h1 {
  color: hsl(213, 96%, 18%);
  font-size: 30px;
}
</style>
