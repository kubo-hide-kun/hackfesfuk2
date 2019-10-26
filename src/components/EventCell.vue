<template>
  <v-card class="mx-auto event-card" outlined width="95%">
    <v-list-item three-line>
      <v-list-item-content class="event-content">
        <div class="overline mb-4">{{owner}}</div>
        <v-list-item-title class="headline mb-1">
          <a><b>{{title}}</b></a>
        </v-list-item-title>
          開催場所: {{place}}<span/>{{startTime}} ~ {{endTime}}
        <div>
          <div v-for="(tag,key) in tags" :key="key" class="tag-chips">
            <v-chip class="ma-1" small>{{tag}}</v-chip>
          </div>
        </div>
      </v-list-item-content>
    </v-list-item>
  </v-card>
</template>

<script>
import moment from "moment"; // eslint-disable-line
export default {
  props: {
    title: {
      type: String,
      default: "タイトル"
    },
    start: {
      type: Date,
      default: new Date("2001-08-02T10:45:23.5+09:00")
    },
    end: {
      type: Date,
      default: new Date("2001-08-02T17:00:00+09:00")
    },
    place: {
      type: String,
      default: "場所"
    },
    tags: {
      type: Array,
      default: () => ["タグ配列1", "タグ配列2", "タグ配列3"]
    },
    owner: {
      type: String,
      default: "主催者の名前"
    },
    nowAttendances: {
      type: Number,
      default: 0
    },
    limitAttendances: {
      type: Number,
      default: 0
    }
  },
  data: () => ({
    starttime: "",
    endTime: ""
  }),
  mounted() {
    this.startTime = moment(this.start).format("MM月DD日 HH:mm");
    this.endTime = moment(this.end).format("HH:mm");
  }
};
</script>
<style scoped>
.event-content {
  font-size: 1em;
}
.tag-chips {
  display: inline;
}
.event-card {
  border-radius: 20px 20px 20px 20px;
  box-shadow: 2px 2px 4px gray;
  margin-bottom: 20px;
}
@media screen and (max-width: 1400px){
  .event-content {
  font-size: 0.85em;
}
}
</style>