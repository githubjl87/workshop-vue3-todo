<script setup>
import { reactive, ref } from 'vue';
import TaskCard from './TaskCard.vue';

const tasks = reactive([])
function addTask(title, description) {
  tasks.unshift({title, description});

}

const newTitle = ref('')
const newDescription = ref('')
const showNewTaskForm = ref(false)
</script>

<template>
  <button class="btn round-icon" @click="showNewTaskForm = !showNewTaskForm">＋</button>
  <div v-show="showNewTaskForm" class="task-card new-task" @keyup.enter="addTask(newTitle, newDescription)">
    <div>
      <input type="text" placeholder="What would you like to do?" v-model="newTitle"/>
      <textarea placeholder="Add some details about your task..." v-model="newDescription"></textarea>
    </div>
  </div>

  <TaskCard v-if="tasks.length > 0" v-for="(task, index) in tasks" :title="task.title" :description="task.description" :done="task.done"/>
    <p v-else>You don't have any task yet...</p>
</template>

<style lang="scss" scoped>
@keyframes expand-vertical { from { min-height: 0; height: 0; } to { min-height: 6rem; } }
.task-card.new-task {
  animation: expand-vertical 0.2s;
  overflow: hidden;
  background-color: white;
  border-left: solid 5px #35495e;
  &, &:hover { transform: scale(1.1); box-shadow: 2px 3px 10px rgba(black, 0.2); }
  & + .tasks-list { pointer-events: none; }
  input { font-size: 1.17rem; font-weight: bold; width: 100%; }
  textarea { width: 100%; font-size: 0.9rem; resize: none; }
}
</style>
