<template>
  <v-app>

  <v-card
    class="mx-auto ma-2"
    width="92%"
    outlined
  >
    <v-list-item three-line>
      <v-list-item-avatar
        tile
        size="200"
        color="grey"
      >
        <v-list-item-title class="headline mb-1 white--text align-end">10月05日</v-list-item-title>
      </v-list-item-avatar>

      <v-list-item-content>
        <div class="overline mb-4">ORNER NAME</div>
        <v-list-item-title class="headline mb-1">Title</v-list-item-title>
        <v-list-item-subtitle>
          <p>開催時刻: 18:30~21:30</p>
          <p>開催場所: 北九州</p>
        <div class="chip-list">
          <div v-for="(tag,key) in tags" :key="key" class="tag-chips">
            <v-chip class="ma-1" small >{{tag}}</v-chip>
          </div>
        </div>
        </v-list-item-subtitle>
      </v-list-item-content>
    </v-list-item>

  </v-card>

  <v-card
    class="mx-auto ma-2"
    width="92%"
    outlined
  >
    <mavon-editor 
      v-model="description"
      language="ja"
      :subfield="false"
      defaultOpen="preview"
      :editable="false"
      :toolbars="false"
    />
  </v-card>
  
  </v-app>
</template>
 
<script>
import Vue from "vue";
import mavonEditor from "mavon-editor";
import "mavon-editor/dist/css/index.css";
Vue.use(mavonEditor);

export default {
  data() {
    return {
      description: "# hackU",
      tags: ["AS","A","zxflkh","sajkg"]
    }
  }
}
</script> 
<style scoped>
.chip-list {
  display: flex;
  flex-wrap: wrap;
}
</style>