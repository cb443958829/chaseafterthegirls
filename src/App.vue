<template>
  <div id="app">
    <MyStudy></MyStudy>
  </div>
</template>

<script>
import myStudy from './components/myStudy.vue'

export default {
  name: 'App',
  components: {
    MyStudy:myStudy
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
  margin-left: 30px;
}
</style>
