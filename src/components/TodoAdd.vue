<template>
  <v-row>
    <v-col cols="10">
      <v-text-field
        name="name"
        label="Task"
        id="id"
        @keyup.enter="addTask"
        v-model="taskTextField"
      ></v-text-field>
    </v-col>
    <v-col>
      <v-btn block color="success" @click="addTask">Add</v-btn>
    </v-col>
  </v-row>
</template>

<script>
import { v1 as uuid } from "uuid";
export default {
  name: "TodoAdd",
  data() {
    return {
      taskTextField: "",
    };
  },

  methods: {
   async addTask() {
      let task = {
        id: uuid(),
        title: this.taskTextField,
        completed: false,
      };

      this.$emit("onsubmit", task);
      this.taskTextField = "";
    },
  },
};
</script>

<style>
</style>