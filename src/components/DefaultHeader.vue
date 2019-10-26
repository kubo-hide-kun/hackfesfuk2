<template>
  <v-app-bar app>
    <v-toolbar-title class="headline">
      <span>Sample Name</span>
    </v-toolbar-title>
    <v-spacer />
    <v-btn
      text
      href="https://github.com/vuetifyjs/vuetify/releases/latest"
      target="_blank"
    >
      <span class="mr-2">ログイン</span>
    </v-btn>
  </v-app-bar>
</template>

<script>
export default {
  name: 'Header',
  data: () => ({
    //
  }),
};
</script>

<style scoped>
.headline {
  margin: 0 20px; 
}
.searchForm {
  width: 425px; 
}
</style>
