<script>
export default {
  name: "App",
  data() {
    return {
      name: "JONH",
      status: "active",
      tasks: ["Task 1", "Task 2", "Task 3"],
      link: "https://www.google.com",
    };
  },
  methods: {
    toggleStatus() {
      if (this.status === "active") {
        this.status = "pending";
      } else if (this.status === "pending") {
        this.status = "inactive";
      } else {
        this.status = "active";
      }
    },
  },
};
</script>

<template>
  <div>
    <h1>vue jobs {{ name }}</h1>
    <p v-if="status === 'active'">User is active</p>
    <p v-else-if="status === 'pending'">User is pending</p>
    <p v-else>User is inactive</p>

    <h3>Tasks:</h3>
    <ul>
      <li v-for="task in tasks" :key="task">{{ task }}</li>
    </ul>
    <a v-bind:href="link" target="_blank">Google</a>
    <a :href="link" target="_blank">Google</a>

    <button v-on:click="toggleStatus">Change Status</button>
    <button @click="toggleStatus">Change Status @</button>
  </div>
</template>

<style scoped>
h1 {
  color: red;
}
</style>
