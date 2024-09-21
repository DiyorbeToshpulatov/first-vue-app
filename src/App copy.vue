<template>
  <h1>Find a Jobs</h1>
  <h2>{{ name }}</h2>
  <p v-if="status">User is active</p>
  <p v-else>User is inactive now</p>
  <button @click="toggleStatus">Change Status</button>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" name="newTask" id="newTask" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>

  <h3>Tasks</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>
        {{ task }}
      </span>
      <button id="btnDelete" @click="removeTask(index)">Delete</button>
    </li>
  </ul>
</template>

<script setup>
import { onMounted, ref } from 'vue';

const name = 'Diyorbek';
const status = ref(true);
const tasks = ref(['Task 1', 'Task 2', 'Task 3', 'Task 4']);

const newTask = ref('');

const toggleStatus = () => {
  status.value = !status.value;
};

function addTask() {
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value);
    newTask.value = '';
  }
}

const removeTask = index => {
  tasks.value.splice(index, 1);
};

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
    const data = await response.json();
    tasks.value = data.map(task => task.title);
  } catch (error) {
    console.log('Error fetching tasks');
  }
});
</script>
