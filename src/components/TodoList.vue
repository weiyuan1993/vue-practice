<template>
<div id="TodoList">
  <!-- 可使用.trim去除空白 -->
  <input type="text" v-bind:placeholder="placeholder" v-model.trim="todoMessage">

  <!-- v-on:click === @click -->
  <button v-on:click="addTodo">Add Todo</button>
  <div id="content">
    <ul>
      <!-- v-bind:key === :key  -->
      <li v-bind:class="todolist-item" v-for="(todo,index) in todoList" v-bind:key="index">
        <input v-bind:id="`todo-${index}`" type="checkbox" v-model="todo.checked">
        <label v-bind:for="`todo-${index}`">{{todo.name}}</label>

      </li>
    </ul>
  </div>

</div>
</template>

<script>
export default {
  name: 'TodoList',
  data() {
    return {
      placeholder: 'Please add something',
      todoMessage: '',
      todoList: [{ name: 'Learn Vue.js', checked: true }]
    }
  },
  methods: {
    addTodo() {
      this.todoList.push({ name: this.todoMessage })
      this.todoMessage = ''
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
#TodoList {
  .todolist {
    &-item {
      &-checked {
        text-decoration: todo;
      }
    }
  }
}
</style>
