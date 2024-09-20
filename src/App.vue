<template>
  <div id="app">
    <task :tasks="tasks" @update:tasks="updateTasks"></task>
  </div>
</template>

<script>
import Task from "./components/Task.vue";

export default {
  name: "App",
  components: {
    Task,
  },
  data() {
    return {
      tasks: this.getSavedTasks(),
    };
  },
  methods: {
    getSavedTasks() {
      // Retrieve tasks from localStorage, if available
      const savedTasks = localStorage.getItem('tasks');
      return savedTasks ? JSON.parse(savedTasks) : this.defaultTasks();
    },
    saveTasks() {
      // Save tasks to localStorage whenever there's a change
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
    defaultTasks() {
      return [
        { id: 1, title: "Learning Python", completed: true },
        { id: 2, title: "Playing Basketball", completed: true },
        { id: 3, title: "Activity 1", completed: false },
        { id: 4, title: "Sleep", completed: false },
        { id: 5, title: "Walk", completed: false },
      ];
    },
    updateTasks(newTasks) {
      this.tasks = newTasks; // Update tasks in App.vue
    },
  },
  watch: {
    tasks: {
      handler() {
        // Watch for changes in tasks and save them
        this.saveTasks();
      },
      deep: true,
    },
  },
};
</script>
