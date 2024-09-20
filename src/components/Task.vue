<template>
  <div class="container">
    <div class="task">
      <!-- title -->
      <header class="title">
        <h1>To Do List</h1>
      </header>
      <!-- form -->
      <section class="form">
        <input
          type="text"
          placeholder="New Task"
          v-model="newTask"
          @keyup.enter="addTask"
          aria-label="Add new task"
        />
        <button @click="addTask" aria-label="Add task">
          <i class="fas fa-plus"></i>
        </button>
      </section>
      <!-- task lists -->
      <section class="taskItems">
        <ul>
          <task-item
            v-for="(task, index) in localTasks"
            :key="task.id"
            :task="task"
            @remove="removeTask(index)"
            @complete="toggleTaskCompletion(task)"
          ></task-item>
        </ul>
      </section>
      <!-- buttons -->
      <footer class="clearBtns">
        <button @click="clearCompleted" aria-label="Clear completed tasks">Clear completed</button>
        <button @click="clearAll" aria-label="Clear all tasks">Clear all</button>
      </footer>
      <!-- pending task -->
      <div class="pendingTasks">
        <span>Pending Tasks: {{ incompleteTasks }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import TaskItem from "./Task-item.vue";

export default {
  name: "Task",
  props: {
    tasks: Array
  },
  components: {
    TaskItem,
  },
  data() {
    return {
      newTask: "",
      localTasks: [...this.tasks], // Create a local copy of tasks
    };
  },
  computed: {
    incompleteTasks() {
      return this.localTasks.filter(task => !task.completed).length;
    },
  },
  methods: {
    addTask() {
      const taskTitle = this.newTask.trim();
      if (taskTitle) {
        this.localTasks.push({
          id: Date.now(), // Use unique ID
          title: taskTitle,
          completed: false,
        });
        this.newTask = ""; // Reset input field
      }
    },
    toggleTaskCompletion(task) {
      task.completed = !task.completed;
    },
    removeTask(index) {
      this.localTasks.splice(index, 1);
    },
    clearCompleted() {
      this.localTasks = this.localTasks.filter(task => !task.completed);
    },
    clearAll() {
      this.localTasks = [];
    },
  },
  watch: {
    localTasks: {
      handler() {
        // Emit updated tasks back to parent
        this.$emit('update:tasks', this.localTasks);
      },
      deep: true,
    },
  },
};
</script>
