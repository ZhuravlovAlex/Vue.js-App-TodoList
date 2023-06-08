<template>
  <div id="app">
    <div class="header">
      <img src="./assets/logo.png" />
      <h1>Todo application</h1>
      <img src="./assets/cadillac.svg" />
    </div>
    <hr />
    <router-view />
  </div>
</template>

<script>
import TodoList from '@/components/TodoList';
import AddTodo from '@/components/AddTodo.vue';
// import { filter } from 'vue/types/umd';
export default {
  name: 'App',
  data() {
    return {
      todosArray: [],
      // todosArray: [
      //   { id: 1, title: 'Купить хлеб', completed: false },
      //   { id: 2, title: 'Купить соль', completed: false },
      //   { id: 3, title: 'Купить масло', completed: false },
      // ],
    };
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then((response) => response.json())
      .then((json) => {
        this.todosArray = json;
      });
  },
  methods: {
    removeTodo(id) {
      // this.todosArray = this.todosArray.splice(id);
      this.todosArray = this.todosArray.filter((t) => t.id !== id);
    },
    addTodo(todo) {
      this.todosArray.push(todo);
    },
  },
  components: {
    TodoList: TodoList,
    AddTodo: AddTodo,
  },
};
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
img {
  width: 100px;
  height: 100px;
}
.header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 36px;
  margin-right: 8%;
  margin-left: 8%;
}
</style>
