<template>
  <div>
    <div class="header">
      <!-- <img src="../assets/logo.png" /> -->
      <h2>Todo application</h2>
      <router-link to="/"> Home</router-link>
      <br />
      <!-- <img src="../assets/cadillac.svg" /> -->
    </div>
    <!-- добавляем прослушиватель  add-todo -->
    <AddTodo @add-todo="addTodo" />
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not Completed</option>
    </select>
    <hr />
    <Loader v-if="loading" />
    <TodoList
      v-else-if="filteredTodos.length"
      v-bind:todosArray="filteredTodos"
      v-on:remove-todo="removeTodo"
    />
    <p v-else>No TODO! / todosArray is empty</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList';
import AddTodo from '@/components/AddTodo.vue';
import Loader from '@/components/Loader.vue';
// import { filter } from 'vue/types/umd';
export default {
  name: 'App',
  data() {
    return {
      todosArray: [],
      loading: true,
      filter: 'all',
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
        setTimeout(() => {
          this.todosArray = json;
          this.loading = false;
        }, 500);
      });
  },
  // watch: {
  //   filter(value) {
  //     console.log(value);
  //   },
  // },
  computed: {
    filteredTodos() {
      if (this.filter === 'all') {
        return this.todosArray;
      }
      if (this.filter === 'completed') {
        return this.todosArray.filter((t) => t.completed);
      }
      if (this.filter === 'not-completed') {
        return this.todosArray.filter((t) => !t.completed);
      }
    },
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
    Loader: Loader,
  },
};
</script>
