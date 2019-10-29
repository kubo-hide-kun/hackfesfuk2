<template>
  <v-app-bar app>
    <router-link to="/">
      <v-toolbar-title class="headline">
        <span>SGMS</span>
      </v-toolbar-title>
    </router-link>
    <v-spacer />
    <router-link to="create">
      <v-btn text target="_blank">
        <span class="mr-2">イベント作成</span>
      </v-btn>
    </router-link>
  </v-app-bar>
</template>

<script>
export default {
  name: "SignedHeader",
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
