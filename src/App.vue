<template>
  <div id="app">
      <Header/>
      <Main/>
      <Footer/>
  </div>
</template>

<script>

import Footer from "@/components/Footer";
import Main from "@/components/Main";
import Header from "@/components/Header";

export default {
  name: 'App',
  components: {
    Header,
    Main,
    Footer
  }
}

</script>

<style lang="scss">
* {
  box-sizing: border-box;
}
#app {
  background-color: #515960;
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  //justify-content: space-between;
  align-items: stretch;
  align-content: stretch;
}
</style>
