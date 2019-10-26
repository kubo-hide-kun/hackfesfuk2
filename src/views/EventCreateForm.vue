<template>
  <v-app>
    <v-container class="event-create-form">
      <v-text-field v-model="title" label="イベント名" outlined></v-text-field>・詳細(MarkDown対応)
      <mavon-editor v-model="detail" language="ja" ref="md" @imgAdd="$imgAdd" />

      <v-row>
        <v-col cols="12" lg="6">
          <v-dialog
            ref="dialog1"
            v-model="startDay"
            :return-value.sync="date1"
            persistent
            width="290px"
          >
            <template v-slot:activator="{ on }">
              <v-text-field v-model="date1" label="開始日" readonly v-on="on"></v-text-field>
            </template>
            <v-date-picker v-model="date1" scrollable>
              <v-spacer></v-spacer>
              <v-btn text color="primary" @click="startDay = false">Cancel</v-btn>
              <v-btn text color="primary" @click="$refs.dialog1.save(date1)">OK</v-btn>
            </v-date-picker>
          </v-dialog>
        </v-col>

        <v-col cols="12" lg="6">
          <v-dialog
            ref="dialog3"
            v-model="startTime"
            :return-value.sync="time1"
            persistent
            width="290px"
          >
            <template v-slot:activator="{ on }">
              <v-text-field v-model="time1" label="開始時刻" readonly v-on="on"></v-text-field>
            </template>
            <v-time-picker v-if="startTime" v-model="time1" full-width>
              <v-spacer></v-spacer>
              <v-btn text color="primary" @click="startTime = false">Cancel</v-btn>
              <v-btn text color="primary" @click="$refs.dialog3.save(time1)">OK</v-btn>
            </v-time-picker>
          </v-dialog>
        </v-col>
      </v-row>

      <v-row>
        <v-col cols="12" lg="6">
          <v-dialog
            ref="dialog2"
            v-model="endDay"
            :return-value.sync="date2"
            persistent
            width="290px"
          >
            <template v-slot:activator="{ on }">
              <v-text-field v-model="date2" label="終了日" readonly v-on="on"></v-text-field>
            </template>
            <v-date-picker v-model="date2" scrollable>
              <v-spacer></v-spacer>
              <v-btn text color="primary" @click="endDay = false">Cancel</v-btn>
              <v-btn text color="primary" @click="$refs.dialog2.save(date2)">OK</v-btn>
            </v-date-picker>
          </v-dialog>
        </v-col>

        <v-col cols="12" lg="6">
          <v-dialog
            ref="dialog4"
            v-model="endTime"
            :return-value.sync="time2"
            persistent
            width="290px"
          >
            <template v-slot:activator="{ on }">
              <v-text-field v-model="time2" label="終了時刻" readonly v-on="on"></v-text-field>
            </template>
            <v-time-picker v-if="endTime" v-model="time2" full-width>
              <v-spacer></v-spacer>
              <v-btn text color="primary" @click="endTime = false">Cancel</v-btn>
              <v-btn text color="primary" @click="$refs.dialog4.save(time2)">OK</v-btn>
            </v-time-picker>
          </v-dialog>
        </v-col>
      </v-row>

      <div width="100%">
        <tr>
          <td width="70%">
            <v-text-field v-model="inputTag" label="追加するタグ" outlined></v-text-field>
          </td>
          <td width="10%">
            <v-btn color="blue" dark class="ma-1" @click="addTag">タグ追加</v-btn>
          </td>
        </tr>
      </div>
      <div class="chip-list">
        <div v-for="(tag,key) in tags" :key="key" class="tag-chips">
          <v-chip class="ma-1" small close @click:close="removeTag(tag)">{{tag}}</v-chip>
        </div>
      </div>
      <v-text-field v-model="limitAttendaces" type="number" label="最大参加者数" outlined class="ma-2"></v-text-field>
      <v-row>
        <v-switch v-model="isPublic" :label="isPublic ? '公開する' : '公開しない'" class="ma-2"></v-switch>
        <v-btn color="blue" dark class="ma-2" @click="post">送信</v-btn>
      </v-row>
    </v-container>
  </v-app>
</template>
 
<script>
import Vue from "vue";
import axios from "axios";
import mavonEditor from "mavon-editor";
import "mavon-editor/dist/css/index.css";
Vue.use(mavonEditor);

export default {
  name: "app",
  data() {
    return {
      title: "",
      detail: "",
      date1: new Date().toISOString().substr(0, 10),
      date2: new Date().toISOString().substr(0, 10),
      time1: null,
      time2: null,
      startDay: false,
      endDay: false,
      startTime: false,
      endTime: false,
      inputTag: "",
      tags: [
        "test1",
        "test2",
        "test3",
        "test",
        "test1",
        "test2",
        "test3",
        "test"
      ],
      limitAttendaces: "",
      isPublic: false
    };
  },
  methods: {
    $imgAdd(pos, $file) {
      var formdata = new FormData();
      formdata.append("image", $file);
      axios({
        url: "https://hackfesfuk-api.azurewebsites.net/api/add-image",
        method: "post",
        data: formdata,
        headers: { "Content-Type": "multipart/form-data" }
      }).then(url => {
        console.log(url); // eslint-disable-line
        mavonEditor.$img2Url(pos, url);
      });
    },
    addTag() {
      if(!this.inputTag) return;
      this.tags.push(this.inputTag);
      this.inputTag = "";
    },
    removeTag(item) {
      this.tags.splice(this.tags.indexOf(item), 1);
      this.tags = [...this.tags];
    },
    post() {
      let url = "https://hackfesfuk-api.azurewebsites.net/api/create-event";
      console.log(url);　//eslint-disable-line
    }
  }
};
</script> 
<style scoped>
.markdown-editor {
  margin: 10px;
  padding: 100px;
  width: 90%;
}
.event-create-form {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  margin-top: 40px;
}
.chip-list {
  display: flex;
  flex-wrap: wrap;
}
</style>