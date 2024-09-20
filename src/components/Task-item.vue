<template>
    <li>
      <!-- Task completion button -->
      <button 
        @click.self="$emit('complete')" 
        :class="['toggle', { 'toggle-completed': task.completed }]"
        aria-label="Mark task as completed or incomplete"
      >
        <i :class="task.completed ? 'far fa-check-circle' : 'far fa-circle'"></i>
        {{ task.title }}
      </button>
  
      <!-- Task removal button -->
      <button 
        @click="$emit('remove')" 
        aria-label="Remove task"
        class="remove-btn"
      >
        <i class="far fa-trash-alt"></i>
      </button>
    </li>
  </template>
  
  <script>
  export default {
    name: "TaskItem",
    props: ["task"]
  };
  </script>
  
  <style scoped>
  /* Style the task list item */
  li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 10px;
  }
  
  /* Toggle button for task completion */
  .toggle {
    display: flex;
    align-items: center;
    background: none;
    border: none;
    cursor: pointer;
  }
  
  .toggle-completed {
    text-decoration: line-through;
    color: gray;
  }
  
  /* Remove button */
  .remove-btn {
    background: none;
    border: none;
    cursor: pointer;
    color: red;
  }
  </style>
  