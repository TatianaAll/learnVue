<!-- composition API -->
<script setup>
import { onMounted, ref } from 'vue';

const name = ref("Tatiana ALLERY");
const status = ref("active");
const tasks = ref(["task 1", "task 2", "task 3", "task 4"]);
const newTask = ref("");

const toogleStatus = () => {
  if (status.value === "active") {
    status.value = "pending";
  } else if (status.value === "pending") {
    status.value = "inactive";
  } else {
    status.value = "active";
  }
};

const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value);
    newTask.value = "";
  }
};
const deleteTask = (index) => {
  tasks.value.splice(index, 1);
}

onMounted(async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos");
    const data = await response.json();
    tasks.value = data.map((task) => task.title);
  } catch (error) {
    console.log("Error fetching tasks");
  }
});
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'"> User is active </p>
  <p v-else-if="status === 'pending'"> The user is pending </p>
  <p v-else> User is inactive </p>

  <!-- @submit for v-on submit et .prevent for prevent the default behaviour -->
  <form @submit.prevent="addTask">
    <label for="newTask">Add task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask">
    <button type="submit">Submit</button>
  </form>

  <h2>Tasks</h2>
  <ul>
    <li v-for="(task, index) in tasks" :key="tasks">
      <span>{{ task }}</span>
      <button @click="deleteTask(index)">X</button>
    </li>
  </ul>
  <br />
  <!-- <button v-on:click="toogleStatus">Changer de statut</button> -->
  <button @click="toogleStatus">Changer de statut</button>
</template>

<style scoped></style>