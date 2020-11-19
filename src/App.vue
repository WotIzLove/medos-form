<template>
  <div id="app">
    <div class="wrapper">
      <div class="container">
        <div class="part card-details">
          <h1 class="main-title">Регистрация</h1>
          <div>
            <Login />
          </div>
        </div>
      </div>
      <div class="part bg"></div>
    </div>
  </div>
</template>

<script>
import Login from "./components/Login.vue";

export default {
  name: "App",
  components: {
    Login,
  },
};
</script>

<style lang="sass">
#app
  font-family: Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  text-align: center
  color: #2c3e50

.container
  display: flex
  margin: 0 auto
  width: 650px
  background-color: #fff
  border-radius: 10px
  padding: 48px 40px
  margin-top: 60px
  margin-bottom: 60px
  .part
    float: left
    height: 100%
    &.card-details
      width: 100%
      h1
        background-color: #00b0ff
        color: white
        font-size: 12px
        text-transform: uppercase
        padding: 14px 0 10px 49px
        letter-spacing: 1px
        margin-left: -70px
        width: 330px
      &.bg
        width: 40%
        background-size: 121%
        background-repeat: no-repeat
        overflow: hidden

@media (max-width: 650px)
  .container
    width: 100%
    border-radius: 0
    margin: 0
</style>
