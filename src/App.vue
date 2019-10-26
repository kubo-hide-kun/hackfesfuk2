<template>
  <v-app>
    <SignedHeader v-if="this.$store.state.isSigned"/>
    <DefaultHeader v-else/>
    <v-content>
      <router-view/>
    </v-content>
  </v-app>
</template>

<script>
import DefaultHeader from './components/DefaultHeader';
import SignedHeader from './components/SignedHeader';

export default {
  name: 'App',
  components: {
    DefaultHeader,
    SignedHeader
  },
  data: () => ({
    //
  }),
};
</script>
