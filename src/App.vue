<template>
  <div>
    <h1>To-Do List</h1>
    <form>
      <label for="name">Name:</label>
      <input type="text" id="name" v-model="newName"><br><br>
      <label for="activity">Task:</label>
      <input type="text" id="activity" v-model="newActivity"><br><br>
      <label for="date">Date:</label>
      <input type="date" id="date" v-model="newDate"><br><br>
      <label for="email">Email:</label>
      <input type="email" id="email" v-model="newEmail"><br><br>
      <button type="button" @click="addActivity">Add</button>
      <button type="button" @click="filterUnfinished">Filter</button>
    </form>
    <ul>
      <li v-for="(activity, index) in activities" :key="index" :style="{textDecoration: activity.completed ? 'line-through' : 'none'}">
        <strong>{{ activity.name }}</strong> - {{ activity.date }} - {{ activity.email }}<br>
        {{ activity.activity }}
        <button @click="removeActivity(index)">Remove</button>
        <button @click="completeActivity(index)" v-if="!activity.completed">Complete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activities: [],
      newName: "",
      newActivity: "",
      newDate: "",
      newEmail: ""
    };
  },
  methods: {
    addActivity() {
      if (this.newActivity !== "") {
        this.activities.push({ 
          name: this.newName, 
          activity: this.newActivity, 
          date: this.newDate, 
          email: this.newEmail, 
          completed: false 
        });
        this.newName = "";
        this.newActivity = "";
        this.newDate = "";
        this.newEmail = "";
      }
    },
    removeActivity(index) {
      this.activities.splice(index, 1);
    },
    completeActivity(index) {
      this.activities[index].completed = true;
    },
    filterUnfinished() {
      this.activities = this.activities.filter(function (activity) {
        return !activity.completed;
      });
    },
  },
};
</script>

<style>
/* Your existing styles */
</style>