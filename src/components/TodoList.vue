<template>
<div id="TodoList">

  <div class= "top-area">
    <!-- 可使用.trim去除空白 -->
    <input type="text" v-bind:placeholder="placeholder" v-model.trim="todoMessage">

    <!-- v-on:click === @click -->
    <button v-on:click="addTodo">Add Todo</button>
    <!-- v-if 不會先渲染 ,v-show 用 display:none -->

  </div>
  <div id="content">
        <div v-if="isMaxLimit">最多只能有{{maxLimit}}筆待辦事項！</div>
    共有: {{todoList.length}} 筆事項，有 {{checkedTodos.length}} 筆完成
    <ol class="todolist">
      <!-- v-bind:key === :key  -->
      <li v-bind:class="[todolist-item,todo.checked?'todolist-item--notshow':'']" v-for="(todo,index) in todoList" v-bind:key="index">
        <input v-bind:id="`todo-${index}`" type="checkbox" v-model="todo.checked">
        <label v-bind:class="{'todolist-item-checked':todo.checked}"
               v-bind:for="`todo-${index}`">{{todo.name}}</label>
        <button @click="removeTodo(index)">X</button>
      </li>
    </ol>
    <!-- {{todoList}} -->

    <div class="checkedList">
      已完成清單：
      <li v-bind:class="todolist-item" v-for="(checkedTodo,index) in checkedTodos" v-bind:key="index">
        {{checkedTodo.name}}
        <button @click="removeTodo(index)">X</button>
      </li>
    </div>
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
      todoList: [{ name: 'Learn Vue.js', checked: false }],
      maxLimit: 3
    }
  },
  computed: {
    checkedTodos() {
      return this.todoList.filter(todo => todo.checked)
    },
    isMaxLimit() {
      return this.todoList.length === this.maxLimit
    }
  },
  methods: {
    addTodo() {
      if (!this.isMaxLimit && this.todoMessage) {
        this.todoList.push({ name: this.todoMessage })
      }
      this.todoMessage = ''
    },
    removeTodo(index) {
      this.todoList.splice(index, 1)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
#TodoList {
  * {
    font-size: 1.2em;
  }
  .top {
    display: flex;

    &-area {
      > * {
        flex: 1;
        flex-basis: 30px;
      }
      display: flex;
      // flex-direction: column;
    }
  }

  .todolist {
    &-item {
      display: flex;
      align-items: center;
      text-align: center;
      &-checked {
        text-decoration: line-through;
      }
      &--notshow {
        display: none;
      }
    }
  }
}
</style>
