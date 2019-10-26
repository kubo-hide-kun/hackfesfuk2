<template>
  <v-app>
    <mavon-editor v-model="value" language="en" />
  <button @click="print">ddd</button>
  </v-app>
</template>
 
<script>
import Vue from "vue";
import mavonEditor from 'mavon-editor';
import "mavon-editor/dist/css/index.css";
Vue.use(mavonEditor);

export default {
  name: "app",
  data() {
    return { value: "" }; 
  },
  methods: {
    print() {
      console.log(this.value);  // eslint-disable-line
      console.log(this);  // eslint-disable-line
    }
  }
};
</script> 