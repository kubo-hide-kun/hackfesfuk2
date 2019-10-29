<template>
  <v-card class="mx-auto event-card" outlined width="95%">
    <v-list-item three-line>
      <v-list-item-content class="event-content">
        <div class="mb-2">
          <a>{{owner}}</a>
        </div>
        <v-list-item-title class="headline mb-1">
          <router-link to="detail">
            <b>{{title}}</b>
          </router-link>
        </v-list-item-title>
        <div v-if="nowAttendances >= limitAttendances">
          参加人数:
          <b>
            <font color="#ff3300">{{nowAttendances}}/{{limitAttendances}}</font>
          </b>
        </div>
        <div v-else>参加人数: {{nowAttendances}}/{{limitAttendances}}</div>
        <span />
        開催場所: {{place}}
        <span />
        {{startTime}} ~ {{endTime}}
        <div>
          <div v-for="(tag,key) in tags" :key="key" class="tag-chips">
            <v-chip
              class="ma-1"
              small
              :color="checkTag(tag)?'':'orange'"
              @click="addTags(tag)"
            >{{tag}}</v-chip>
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
      type: String,
      default: "2001-08-02T10:45:23.5+09:00"
    },
    end: {
      type: Date,
      default: "2001-08-02T17:00:00+09:00"
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
    startTime: "",
    endTime: ""
  }),
  mounted() {
    this.startTime = moment(this.start).format("MM月DD日 HH:mm");
    this.endTime = moment(this.end).format("HH:mm");
  },
  methods: {
    addTags(tag) {
      if (this.checkTag(tag)) this.$store.state.myWants.push(tag);
      else
        this.$store.state.myWants = this.$store.state.myWants.filter(
          want => want !== tag
        );
    },
    checkTag(tag) {
      return this.$store.state.myWants.indexOf(tag) == -1;
    }
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
@media screen and (max-width: 1400px) {
  .event-content {
    font-size: 0.85em;
  }
}
</style>