<template>
    <div class="bg-white shadow-md rounded-lg p-6 mb-4">
      <h2 class="text-2xl font-bold text-primary mb-4">Adicione uma nova tarefa</h2>
      <form @submit.prevent="addTodo">
        <div class="mb-4">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="title">Title:</label>
          <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" type="text" v-model="title" id="title" required>
        </div>
        <div class="mb-4">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="description">Description:</label>
          <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" type="text" v-model="description" id="description">
        </div>
        <div class="mb-4">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="dueDate">Due Date:</label>
          <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" type="date" v-model="dueDate" id="dueDate">
        </div>
        <div class="flex items-center justify-between">
          <button class="bg-primary hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="submit">Add Task</button>
        </div>
      </form>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        title: '',
        description: '',
        dueDate: ''
      };
    },
    methods: {
      async addTodo() {
        try {
          const newTodo = {
            title: this.title,
            description: this.description,
            dueDate: this.dueDate,
            completed: false
          };
          await axios.post('http://localhost:5000/api/todos', newTodo);
          this.$emit('todo-added');
          this.title = '';
          this.description = '';
          this.dueDate = '';
        } catch (error) {
          console.error(error);
        }
      }
    }
  }
  </script>
  