<template>
  <div class="header">
    <h2>Тестовое на Vue.js</h2>
  </div>
</template>

<script>
export default {
  name: "header"
}
</script>

<style scoped lang="scss">
.header {
  text-align: center;
  color: #000;
  background-color: darkcyan;
  height: 15vh;
  display: flex;
  align-items: center;
  h2 {
    margin: 0 auto;
  }
}
</style>
