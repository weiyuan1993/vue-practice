<template>
<div id="TodoList">
  <Header :titleName="titleName" v-on:headerChange="getNewHeader"></Header>

  <div class= "top-area">
    <!-- 可使用.trim去除空白 -->
    <input type="text" @keydown.enter="addTodo" v-bind:placeholder="placeholder" v-model.trim="todoMessage">

    <!-- v-on:click === @click -->
    <button v-on:click="addTodo">Add Task</button>
    <!-- v-if 不會先渲染 ,v-show 用 display:none -->
    <button @click="showTodos = true">My Tasks</button>
    <button @click="showTodos = false;">Done</button>

  </div>
  <div id="content">
        <div v-if="isMaxLimit">最多只能有{{maxLimit}}筆待辦事項！</div>
    <div v-if="showTodos" id="todoDiv">
      <h3>待辦清單</h3>
      <div>共有: {{todoList.length}} 筆事項，有 {{checkedTodos.length}} 筆完成</div>

      <ol class="todolist">

        <!-- v-bind:key === :key  -->
        <li v-bind:class="[todolist-item,todo.checked?'todolist-item--notshow':'']" v-for="(todo,index) in todoList" v-bind:key="index">
          <input v-bind:id="`todo-${index}`" type="checkbox" v-model="todo.checked">
          <span v-show="todo.checked">✔️</span>
          <label v-bind:class="{'todolist-item-checked':todo.checked}"
                v-bind:for="`todo-${index}`">{{todo.name}}</label>
          <button @click="removeTodo(index)">remove</button>
        </li>
      </ol>
    </div>
    <div v-if="!showTodos" id="completedDiv">
      <!-- {{todoList}} -->
      <div  class="checkedList">
        <h3>已完成清單：</h3>
        <ol>
          <li v-bind:class="todolist-item" v-for="(checkedTodo,index) in checkedTodos" v-bind:key="index">
            {{checkedTodo.name}}
            <button @click="removeTodo(index)">X</button>
          </li>
        </ol>
      </div>
    </div>
  </div>

</div>
</template>

<script>
import Header from '@/components/Header'

export default {
  name: 'TodoList',
  components: {
    Header
  },
  data() {
    return {
      titleName: `Vue.js TodoList 練習`,
      placeholder: 'Please add something',
      todoMessage: '',
      todoList: [{ name: 'Learn Vue.js', checked: false }, { name: 'Eat breakfast', checked: true }],
      maxLimit: 10,
      showTodos: true
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
    },
    getNewHeader(msg) {
      this.titleName = msg
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
#TodoList {
  border: 1px solid black;

  width: 600px;
  height: auto;
  margin: 0 auto;

  .top {
    &-area {
      display: flex;
      input {
        flex: 8;
      }
      button {
        flex: 2;
      }
      button:hover {
        background-color: aqua;
      }
    }
  }

  .todolist {
    &-item {
      &-checked {
        text-decoration: line-through;
      }
      &--notshow {
        display: none !important;
      }
    }
  }
}
</style>
