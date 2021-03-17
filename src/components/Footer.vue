<template>
  <div class="footer">
    <h4>Copyright &copy; Прудников Андрей Владимирович</h4>
    <span>Моя страничка <a href="https://github.com/AndreyPrudnikoff">Github</a></span>
  </div>
</template>

<script>
export default {
  name: "footer"

}
</script>

<style scoped lang="scss">
.footer {
  text-align: center;
  background-color: #276899;
  color: #fff;
  height: 15vh;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  h4 {
    margin: 0 auto;
  }
  a {
    color: #000;
    text-decoration: underline;
  }
}
</style>
