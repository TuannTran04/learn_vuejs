<script setup>
import { ref, onMounted } from "vue";

const name = ref("John doe");
const status = ref("active");
const tasks = ref(["Task 1", "Task 2", "Task 3"]);
const newTask = ref("");
console.log("task", tasks.value);

const toggleStatus = () => {
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
};

onMounted(async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/posts");
    const data = await response.json();
    console.log(data);
    tasks.value = data.map((item) => item.title);
    console.log("task", tasks.value);
  } catch (error) {
    console.error("Error fetching data:", error);
  }
});
</script>

<template>
  <div>
    <h1>vue jobs {{ name }}</h1>
    <p v-if="status === 'active'">User is active</p>
    <p v-else-if="status === 'pending'">User is pending</p>
    <p v-else>User is inactive</p>

    <form @submit.prevent="addTask">
      <label for="newTask">Add Task</label>
      <input type="text" id="newTask" name="newTask" v-model="newTask" />
      <button type="submit">Submit</button>
    </form>

    <h3>Tasks:</h3>
    <ul>
      <li v-for="(task, index) in tasks" :key="task">
        <span>{{ task }}</span>
        <button @click="deleteTask(index)">x</button>
      </li>
    </ul>
    <!-- <a v-bind:href="link" target="_blank">Google</a>
    <a :href="link" target="_blank">Google</a> -->

    <!-- <button v-on:click="toggleStatus">Change Status</button> -->
    <button @click="toggleStatus">Change Status @</button>
  </div>
</template>

<style scoped>
h1 {
  color: red;
}
</style>
