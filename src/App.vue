<template>
  <v-app>
    <v-app-bar app dark>
      <div class="d-flex align-center">
        <v-icon class="mr-2">calendar_today</v-icon>
        <h1>TodoList</h1>
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>open_in_new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main class="backgroundColor">
      <todoList />
    </v-main>
  </v-app>
</template>

<script>
import todoList from "../views";

export default {
  name: "App",

  components: { todoList },

  data: () => ({
    //
  }),
};
</script>
<style>
.backgroundColor {
  background-color: #dcedc8;
}
</style>