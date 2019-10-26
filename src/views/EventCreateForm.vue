<template>
  <v-app>
    <v-container class="event-create-form">
      <v-row no-gutters wrap>
        <div width="50%">
          <v-card
            class="pa-2 mb-6"
            outlined
            tile
            width="100%"
            :color="isForm ? 'light-blue' : ''"
            :elevation="isForm ? -1 : 2"
            @click="isForm = true"
          >
            <font size="2.5em">イベントの作成</font>
          </v-card>
        </div>
        <div width="50%">
          <v-card
            class="pa-2 mb-6"
            outlined
            tile
            width="100%"
            :color="!isForm ? 'light-blue' : ''"
            :elevation="!isForm ? -1 : 2"
            @click="isForm = false"
          >
            <font size="2.5em">トレンドの確認</font>
          </v-card>
        </div>
      </v-row>
      <div v-if="isForm">
        <v-text-field v-model="title" label="イベント名" outlined></v-text-field>・詳細(MarkDown対応)
        <mavon-editor v-model="description" language="ja" ref="md" @imgAdd="$imgAdd" />

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

        <v-text-field v-model="area" label="開催場所" outlined></v-text-field>
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
      </div>
      <div v-else class="pie-chart">
        <pie-chart :data="chartData" :options="chartOptions"></pie-chart>
      </div>
    </v-container>
  </v-app>
</template>
 
<script>
import Vue from "vue";
import axios from "axios";
import PieChart from "../components/PieChart";
import mavonEditor from "mavon-editor";
import "mavon-editor/dist/css/index.css";
Vue.use(mavonEditor);

export default {
  name: "app",
  components: {
    PieChart
  },
  data() {
    return {
      isForm: true,
      title: "",
      description: "",
      date1: new Date().toISOString().substr(0, 10),
      date2: new Date().toISOString().substr(0, 10),
      time1: null,
      time2: null,
      startDay: false,
      endDay: false,
      startTime: false,
      endTime: false,
      area: "",
      inputTag: "",
      tags: [],
      limitAttendaces: "",
      isPublic: false,
      chartOptions: {
        hoverBorderWidth: 20
      },
      chartData: {
        hoverBackgroundColor: "red",
        hoverBorderWidth: 10,
        labels: ["Green", "Red", "Blue"],
        datasets: [
          {
            label: "Data One",
            backgroundColor: ["#41B883", "#E46651", "#00D8FF"],
            data: [1, 10, 5]
          }
        ]
      }
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
      if (!this.inputTag) return;
      this.tags.push(this.inputTag);
      this.inputTag = "";
    },
    removeTag(item) {
      this.tags.splice(this.tags.indexOf(item), 1);
      this.tags = [...this.tags];
    },
    post() {
      // let url = "https://hackfesfuk-api.azurewebsites.net/api/create-event";

      const XHR = new XMLHttpRequest();
      const FD = new FormData();
      FD.append("title", this.title);
      FD.append("description", this.description);
      FD.append("start", new Date(this.date1 + "T" + this.time1 + "+09:00"));
      FD.append("end", new Date(this.date2 + "T" + this.time2 + "+09:00"));
      FD.append("place", this.area);
      FD.append("tags", this.tags.join(" "));
      FD.append("limitAttendaces", this.limitAttendaces);
      FD.append("public", this.isPublic);

      XHR.open("GET", "https://hackfesfuk-api.azurewebsites.net/api/edit-event");

      XHR.send(FD);
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
.pie-chart {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>