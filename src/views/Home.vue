<template>
  <div>
    <v-container>
      <TodoAdd @onsubmit="addTask" />
      <TodoList :todos="todos | reverseTodo" @onremove="onDelete" />
    </v-container>
  </div>
</template>

<script>
// @ is an alias to /src
import TodoList from "@/components/TodoList.vue";
import TodoAdd from "@/components/TodoAdd.vue";
import axios from "axios";
export default {
  name: "Home",
  components: {
    TodoList,
    TodoAdd,
  },
  async mounted() {
    let result = await axios.get("https://jsonplaceholder.typicode.com/todos");
    this.todos = result.data;
  },

  methods: {
    async addTask(task) {
      let result = await axios.post(
        "https://jsonplaceholder.typicode.com/todos",
        task
      );
      this.todos.push(result.data);
      console.log(task);
      console.log(result.data);
    },
    async onDelete(id) {
      await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`);

      this.todos = this.todos.filter((item) => item.id !== id);
    },
  },
  computed: {
    reverseTodo() {
      return this.todos.slice().reverse();
    },
  },
  filters: {
    reverseTodo(value) {
      return value.slice().reverse();
    },
  },

  data() {
    return {
      todos: [],
      todoMockup: [
        { id: 1, title: "Task 1", completed: false },
        { id: 2, title: "Task 2", completed: true },
        { id: 3, title: "Task 3", completed: false },
      ],
    };
  },
};
</script>
