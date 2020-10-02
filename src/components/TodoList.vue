<template>
  <v-card>
    <v-card-title primary-title>
      <v-container>
        <v-row
          class="d-flex flex-row align-center"
          v-for="(item, index) in todos"
          :key="index"
        >
          <v-col cols="12" class="d-flex flex-row">
            <v-checkbox v-model="item.completed" ></v-checkbox>
            <span>{{ item.title }}</span>
            <v-spacer> </v-spacer>
            <v-btn depressed color="error" @click="onDelete(item.id)">x</v-btn>
          </v-col>
          <v-col cols="12">
            <v-divider> </v-divider>
          </v-col>
        </v-row>
      </v-container>
    </v-card-title>
  </v-card>
</template>

<script>
export default {
  name: "TodoList",
  props: ["todos"],
  methods: {
      onDelete(id) {
          this.$emit('onremove' , id)
      }
  },
};
</script>

<style>
</style>