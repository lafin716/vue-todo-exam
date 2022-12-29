<template>
  <div id="app">
    <TodoHeader />
    <TodoInput v-on:addTodo="addTodo" />
    <TodoList v-bind:propsdata="todoItems" @removeTodo="removeTodo"/>
    <TodoFooter v-on:removeAll="clearAll"/>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue';
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
import TodoFooter from './components/TodoFooter.vue';

export default {
  props: ['propsdata'],
  data() {
    return {
      todoItems: [],
    }
  },
  components: {
    'TodoHeader': TodoHeader,
    'TodoInput': TodoInput,
    'TodoList': TodoList,
    'TodoFooter': TodoFooter,
  },
  methods: {
    addTodo(todoItem) {
      this.todoItems.push(todoItem);
      localStorage.setItem('todoItems', this.todoItems);
    },
    clearAll() {
        localStorage.clear();
        this.todoItems = [];
    },
    removeTodo(index) {
        this.todoItems.splice(index, 1);
        localStorage.setItem('todoItems', this.todoItems);
    } 
  },
  created() {
      let rawTodoItems = localStorage.getItem('todoItems');
      if (rawTodoItems == null || rawTodoItems == '') {
          return;
      }

      let items = rawTodoItems.split(',');
      if (items != null && items.length > 0) {
          for (var i = 0; i < items.length; i++) {
              this.todoItems.push(items[i]);
          }
      }

      console.log(items);
      console.log(this.todoItems);
  },
}
</script>

<style>
  body {
      text-align: center;
      background-color: #F6F6F8;
  }

  input {
      border-style: groove;
      width: 200px;
  }

  button {
      border-style: groove;
  }

  .shadow {
      box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
  }
</style>
