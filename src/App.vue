<template>
  <v-app>
    <DefaultHeader/>
    <v-content>
      <HelloWorld/>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';
import DefaultHeader from './components/DefaultHeader';

export default {
  name: 'App',
  components: {
    HelloWorld,
    DefaultHeader
  },
  data: () => ({
    //
  }),
};
</script>
