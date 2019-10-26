<template>
  <v-app>
    <SignedHeader v-if="this.$store.state.isSigned"/>
    <DefaultHeader v-else/>
    <v-content>
      <HelloWorld/>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';
import DefaultHeader from './components/DefaultHeader';
import SignedHeader from './components/SignedHeader';

export default {
  name: 'App',
  components: {
    HelloWorld,
    DefaultHeader,
    SignedHeader
  },
  data: () => ({
    //
  }),
};
</script>
