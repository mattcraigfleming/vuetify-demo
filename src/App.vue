<template>
  <v-app id="app">
  <v-toolbar>
    <v-toolbar-title>Toolbar</v-toolbar-title>
  </v-toolbar>
  <main>
    <v-content>
      <v-container fluid>
        <router-view></router-view>
      </v-container>
    </v-content>
  </main>
  <v-footer>Footer</v-footer>
</v-app>
</template>

<script>
export default {
  name: 'app',
};
</script>

<style scoped>
  #app {
    display:flex;
    flex-direction: column;
  }

</style>
