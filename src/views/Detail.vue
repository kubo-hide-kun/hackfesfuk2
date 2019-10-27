<template>
  <v-app>
    <v-card class="mx-auto ma-2" width="92%" outlined>
      <v-list-item three-line>
        <v-list-item-avatar tile size="200" color="grey">
          <v-list-item-title class="headline mb-1 white--text align-end">{{startDate}}</v-list-item-title>
        </v-list-item-avatar>

        <v-list-item-content>
          <div class="overline mb-4">{{owner}}</div>
          <v-list-item-title class="headline mb-1">{{title}}</v-list-item-title>
          <div v-if="nowAttendances >= limitAttendances">
            参加人数:
            <b>
              <font color="#ff3300">{{nowAttendances}}/{{limitAttendances}}</font>
            </b>
          </div>
          <div v-else>参加人数: {{nowAttendances}}/{{limitAttendances}}</div>
          <v-list-item-subtitle>
            <p>開催時刻: {{startTime}}~{{endTime}}</p>
            <p>開催場所: {{place}}</p>
            <div class="chip-list">
              <div v-for="(tag,key) in tags" :key="key" class="tag-chips">
                <v-chip
                  class="ma-1"
                  small
                  :color="checkTag(tag)?'':'orange'"
                  @click="addTags(tag)"
                >{{tag}}</v-chip>
              </div>
            </div>
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>
    </v-card>

    <v-card class="mx-auto ma-2" width="92%" outlined>
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
import moment from "moment";
import mavonEditor from "mavon-editor";
import "mavon-editor/dist/css/index.css";
Vue.use(mavonEditor);

export default {
  data() {
    return {
      title: "タイトル",
      description: "# HACKFESFUK",
      start: "2001-08-02T10:45:23.5+09:00",
      end: "2001-08-02T17:00:00+09:00",
      place: "場所",
      tags: ["タグ配列1", "タグ配列2", "タグ配列3"],
      owner: "主催者の名前",
      nowAttendances: 0,
      limitAttendances: 0,
      startDate: "",
      startTime: "",
      endTime: ""
    };
  },
  mounted() {
    this.startDate = moment(this.start).format("MM月 DD日");
    this.startTime = moment(this.start).format("HH:mm");
    this.endTime = moment(this.end).format("HH:mm");
  },
  methods: {
    addTags(tag) {
      if(this.checkTag(tag)) this.$store.state.myWants.push(tag);
      else this.$store.state.myWants = this.$store.state.myWants.filter(want => want!==tag)
    },
    checkTag(tag) {
      return this.$store.state.myWants.indexOf(tag) == -1
    }
  }
};
</script> 
<style scoped>
.chip-list {
  display: flex;
  flex-wrap: wrap;
}
</style>