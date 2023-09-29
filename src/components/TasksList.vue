<script setup>
import { reactive, ref } from 'vue';
import TaskCard from './TaskCard.vue';

const tasks = reactive([])
function addTask(title, description) {
  tasks.unshift({title, description});

}

const newTitle = ref('')
const newDescription = ref('')
</script>

<template>
  <button class="btn round-icon" @click="addTask(newTitle, newDescription)">＋</button>
  <div class="task-card new-task">
    <div>
      <input type="text" placeholder="What would you like to do?" />
      <textarea placeholder="Add some details about your task..."></textarea>
    </div>
  </div>

  <TaskCard v-if="tasks.length > 0" v-for="(task, index) in tasks" :title="task.title" :description="task.description" :done="task.done"/>
    <p v-else>You don't have any task yet...</p>
</template>
