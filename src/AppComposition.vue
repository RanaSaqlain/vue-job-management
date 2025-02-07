<script setup>
import { ref, onMounted } from "vue";

const name = ref("RMS");
const status = ref("active");
const Tasks = ref(["T1", "T2", "T3"]);
const newTask = ref("");
const toggleStatus = () => {
  if (status.value == "active") {
    status.value = "inactive";
  } else if (status.value == "inactive") {
    status.value = "active";
  } else {
    status.value = "something";
  }
};

const addTask = () => {
  if (newTask.value.trim() !== "") {
    Tasks.value.push(newTask.value);
    newTask.value = "";
  }
};

const deleteTask = (index) => {
  Tasks.value.splice(index, 1);
};

onMounted(async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos");
    const data = await response.json();
    Tasks.value = data.map((task) => task.title);
  } catch (error) {
    console.log("errors");
  }
});
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status == 'active'">User is active</p>
  <p v-else-if="status === 'inactive'">User is inactive</p>
  <p v-else>User</p>

  <form @submit.prevent="addTask">
    <label for="">Add Task</label>
    <input type="text" name="newTask" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>

  <h2>Tasks</h2>
  <ul>
    <li v-for="(task, index) in Tasks" :key="task">
      <span>
        {{ task }}
      </span>
      <button @click="deleteTask(index)">x</button>
    </li>
  </ul>
  <a :href="link">A</a>
  <br />
  <button @click="toggleStatus()">Change Status</button>
</template>
