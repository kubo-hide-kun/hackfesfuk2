<template>
  <v-app>
    <SignedHeader v-if="this.$store.state.isSigned"/>
    <DefaultHeader v-else/>
    <v-content>
      <Home/>
    </v-content>
  </v-app>
</template>

<script>
import Home from './views/Home';
import DefaultHeader from './components/DefaultHeader';
import SignedHeader from './components/SignedHeader';

export default {
  name: 'App',
  components: {
    Home,
    DefaultHeader,
    SignedHeader
  },
  data: () => ({
    //
  }),
};
</script>
