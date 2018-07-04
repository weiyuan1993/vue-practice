<template>
  <div id="app">
    <div id="appHeader"><h1>Vue.js Practice</h1></div>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style lang="scss" scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  // margin-top: 60px;
}
#appHeader {
  width: 100%;
  height: 100%;
  background-color: #4a90e2;
  margin-bottom: 10px;
  h1 {
    margin: 0;
  }
}
</style>
