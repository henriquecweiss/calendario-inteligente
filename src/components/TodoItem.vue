<template>
    <div :class="['todo-item', { 'bg-accent': isCompleted, 'bg-secondary': !isCompleted }]">
      <h3 class="text-lg font-semibold text-dark">{{ todo.title }}</h3>
      <p class="text-gray-700">{{ todo.description }}</p>
      <p class="text-gray-500">{{ todo.dueDate }}</p>
      <button @click="toggleComplete" class="mt-2 bg-dark hover:bg-orange-600 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline">
        {{ isCompleted ? 'Mark as Incomplete' : 'Mark as Complete' }}
      </button>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    props: {
      todo: Object
    },
    data() {
      return {
        isCompleted: this.todo.completed
      };
    },
    methods: {
      async toggleComplete() {
        this.isCompleted = !this.isCompleted;
        try {
          await axios.put(`http://localhost:5000/api/todos/${this.todo._id}`, {
            completed: this.isCompleted
          });
          this.$emit('update');
        } catch (error) {
          console.error(error);
        }
      }
    }
  }
  </script>
  