<template>
  <div>
    <h3>Here is TodoList</h3>
    <ul>
      <TodoItem
        v-for="(todo, i) of todosArray"
        v-bind:todo="todo"
        v-bind:index="i"
        v-on:remove-todo="removeTodo"
      />
    </ul>
  </div>
</template>

<script>
import TodoItem from '@/components/TodoItem';
export default {
  props: ['todosArray'],

  components: {
    TodoItem: TodoItem,
  },
  methods: {
    removeTodo(id) {
      this.$emit('remove-todo', id);
    },
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
