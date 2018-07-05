<template>
  <div id="header">
      <h2>{{titleName}}</h2>
      <div>
        Change header(Header.vue $emit to TodoList.vue)
        <input type="text" v-model="msg" @change="inputChange" @keyup="inputChange">
        </div>
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
#header {
  border-bottom: 1px solid black;
}
</style>
