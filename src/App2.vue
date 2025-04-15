<script>
export default {
  data() {
    return {
      name: "Tatiana ALLERY",
      status: "active",
      tasks: ["task 1", "task 2", "task 3", "task 4"],
      link: "https://github.com/TatianaAll",
    };
  },
  methods: {
    toogleStatus() {
      if(this.status === "active") {
         this.status = "pending";
      } else if (this.status === "pending") {
         this.status = "inactive";
      } else {
        this.status = "active";
      }
    },
  }
}
</script>

<template>
  <h1>{{ name }}</h1>
  <ul>
    <li v-for="task in tasks" :key="tasks">
      {{ task }}
    </li>
  </ul>
  <p v-if="status === 'active'">
    User is active
  </p>
  <p v-else-if="status === 'pending'">
    The user is pending
  </p>
  <p v-else>
    User is inactive
  </p>
  <!-- <a v-bind:href="link" target="_blank">Mon github</a> -->
  <a :href="link" target="_blank">Mon github</a>
  <br/>
  <!-- <button v-on:click="toogleStatus">Changer de statut</button> -->
  <button @click="toogleStatus">Changer de statut</button>
</template>

<style scoped></style>