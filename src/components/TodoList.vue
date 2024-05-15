<template>
    <div>
      <h2 class="text-3xl font-bold text-dark mb-6">Calendário Inteligente</h2>
      <AddTodo @todo-added="fetchTodos" />
      <div v-for="todo in todos" :key="todo._id" :class="['shadow-md rounded-lg p-4 mb-4', { 'bg-accent': todo.completed, 'bg-secondary': !todo.completed }]">
        <TodoItem :todo="todo" @update="fetchTodos" />
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  import TodoItem from './TodoItem.vue';
  import AddTodo from './AddTodo.vue';
  
  export default {
    components: {
      TodoItem,
      AddTodo
    },
    data() {
      return {
        todos: []
      };
    },
    created() {
      this.fetchTodos();
    },
    methods: {
      async fetchTodos() {
        try {
          const response = await axios.get('http://localhost:5000/api/todos');
          this.todos = response.data;
        } catch (error) {
          console.error(error);
        }
      }
    }
  }
  </script>
  