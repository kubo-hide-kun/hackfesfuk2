<template>
  <v-app>
    <v-app-bar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Vuetify</span>
        <span class="font-weight-light">MATERIAL DESIGN</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
        text
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
      >
        <span class="mr-2">Latest Release</span>
      </v-btn>
    </v-app-bar>

    <v-content>
      <PropsPractice msg="sample"/>
    </v-content>
  </v-app>
</template>

<script>
import PropsPractice from './views/PropsPractice';

export default {
  name: 'App',
  components: {
    PropsPractice,
  },
  data: () => ({
    //
  }),
};
</script>
