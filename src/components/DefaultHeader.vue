<template>
  <v-app-bar app>
    <v-toolbar-title class="headline">
    <router-link to="/">
      <span>Sample Name</span>
    </router-link>
    </v-toolbar-title>
    <v-spacer />
    <router-link to="signin">
      <v-btn text target="_blank">
        <span class="mr-2">ログイン</span>
      </v-btn>
    </router-link>
  </v-app-bar>
</template>

<script>
export default {
  name: "DefaultHeader",
  data: () => ({
    //
  })
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
