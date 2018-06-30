<template>
  <div id="header">
      <h1>{{titleName}}</h1>
      <div>更換標題(子元件Header 傳向父元件 TodoList)<input type="text" v-model="msg" @change="inputChange" @keyup="inputChange"></div>
  </div>
</template>
<script>
export default {
  name: 'Header',
  data() {
    return {
      header: 'Vue.js TodoList',
      msg: ''
    }
  },
  props: {
    titleName: {
      type: String,
      default: '預設標題'
    }
  },
  methods: {
    inputChange() {
      this.$emit('headerChange', this.msg)
    }
  }
}
</script>
<style scoped>
</style>
