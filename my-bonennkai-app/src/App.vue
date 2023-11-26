<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <DinosaurAnimation />
</template>

<script>
import DinosaurAnimation from './components/DinosaurAnimation.vue'

export default {
  name: 'App',
  components: {
    DinosaurAnimation
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

