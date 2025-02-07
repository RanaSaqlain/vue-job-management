<script>
export default {
  data() {
    return {
      name: "RMS",
      status: "inactive",
      Tasks: ["T1", "T2", "T3"],
      link: "google.com",
    };
  },
  methods: {
    toggleStatus() {
      if (this.status === "active") {
        this.status = "inactive";
      } else if (this.status == 'inactive')
      {
        this.status = 'active'
      }else
      {
        this.status = "something"
      }
    },
  },
};
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status == 'active'">User is active</p>
  <p v-else-if="status === 'inactive'">User is inactive</p>
  <p v-else>User</p>
  <h2>Tasks</h2>
  <ul>
    <li v-for="task in Tasks" :key="task">{{ task }}</li>
  </ul>
  <a :href="link">A</a>
  <br>
  <button @click="toggleStatus()">Change Status</button>
</template>
