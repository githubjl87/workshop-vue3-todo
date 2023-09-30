<script setup>
import { reactive, ref, watch } from 'vue';
import TaskCard from './TaskCard.vue';
import NewTask from './NewTask.vue';


const tasks = reactive(JSON.parse(localStorage.getItem("tasks")) || [])

watch(tasks, (newX) => {
  localStorage.setItem("tasks", JSON.stringify(tasks));
})

function clearTasks() {
  tasks.splice(0)
}

function addTask(title, description) {
  tasks.unshift({title, description});

}

function toggleTask(taskIndex) {
  const taskToUpdate = tasks[taskIndex];
  taskToUpdate.done = !taskToUpdate.done;
}

const showNewTaskForm = ref(false)


</script>

<template>
  <button class="btn round-icon" @click="showNewTaskForm = !showNewTaskForm">＋</button>
  <button class="btn round-icon" @click="clearTasks()">delete all</button>

  <NewTask v-show="showNewTaskForm" @add-task="addTask" />


  <TaskCard v-if="tasks.length > 0" v-for="(task, index) in tasks" :key="index" :title="task.title" :description="task.description" :done="task.done" :task-index="index" @toggle-task="toggleTask"/>
    <p v-else>You don't have any task yet...</p>
</template>

<style lang="scss" scoped>
.clear-tasks {
  font-size: 0.8em;
  cursor: pointer;
  margin: 2em;
  color: #aaa;

  &:hover {
    color: #41b883;
  }
}
</style>
