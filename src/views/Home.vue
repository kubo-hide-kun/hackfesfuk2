<template>
  <v-app>
    <v-layout wrap>
      <v-flex>
        <div id="app" class="pa-0 ma-0">
          <v-app id="inspire" class="pa-0 ma-0">
            <svg height="80" wlass="pa-0 ma-0">
              <ellipse cx="50%" cy="30%" rx="60%" ry="70%" fill="#1867c0" />
              <g font-family="sans-serif" fill="white" font-size="200%">
                <text x="50%" y="65%" text-anchor="middle">Sample Name</text>
              </g>
            </svg>

            <v-flex v-if="mediaQuery" class="pr-0 pl-0 flex-parallax">
              <v-img
                class="pr-5 pl-5 pt-0 parallax"
                src="https://drive.google.com/uc?export=view&id=1TWZJTRd6uNoDk6Ffr2Qd5g96zFJdShbe"
              >
                <div>
                  <v-row>
                    <v-col v-for="card in cards" :key="card.title" :cols="card.flex">
                      <v-flex>
                        <v-card height="300px" width="400px">
                          <v-img
                            :src="card.src"
                            class="white--text"
                            height="200px"
                            width="100%"
                            gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
                          >
                            <v-card-title class="fill-height align-end" v-text="card.title"></v-card-title>
                          </v-img>
                          <v-card-text class="text--primary" v-text="card.text"></v-card-text>
                        </v-card>
                      </v-flex>
                    </v-col>
                  </v-row>
                </div>
              </v-img>
              <EventCell />
              <EventCell />
              <EventCell />
            </v-flex>

            <v-flex class="pr-0 pl-0 flex-parallax" v-else>
              <v-parallax
                class="pr-5 pl-5 pt-0 parallax"
                src="https://drive.google.com/uc?export=view&id=1TWZJTRd6uNoDk6Ffr2Qd5g96zFJdShbe"
              >
                <div>
                  <v-row>
                    <v-col v-for="card in cards" :key="card.title" :cols="card.flex">
                      <v-flex>
                        <v-card height="300px" width="400px">
                          <v-img
                            :src="card.src"
                            class="white--text"
                            height="200px"
                            width="100%"
                            gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
                          >
                            <v-card-title class="fill-height align-end" v-text="card.title"></v-card-title>
                          </v-img>
                          <v-card-text class="text--primary" v-text="card.text"></v-card-text>
                        </v-card>
                      </v-flex>
                    </v-col>
                  </v-row>
                </div>
              </v-parallax>
              <EventCell />
              <EventCell />
              <EventCell />
            </v-flex>
          </v-app>
        </div>
      </v-flex>
    </v-layout>
  </v-app>
</template>

<script>
import EventCell from '../components/EventCell'
export default {
  components: {
    EventCell
  },
  data: () => ({
    dialog: false,
    mediaQuery: false,
    cards: [
      {
        title: "勉強会の作成/告知",
        src:
          "https://drive.google.com/uc?export=view&id=1MGgyDgQ1XwfC9u_WoCFlvXeQyYZlOm8B",
        text:
          "学内の学生に対してイベントの作成及び告知が可能です。イベント状況はこのサイトで確認可能です。"
      },
      {
        title: "より詳細の参加状況",
        src:
          "https://drive.google.com/uc?export=view&id=1rDpAT-QK6hzex-6VV35wTpevAbJnpdyG",
        text:
          "各学生の既読状況を取得する事によって学内の人のイベントへの参加状況を既存サービスより確認出来ます。"
      },
      {
        title: "コミュニティの属性を可視化",
        src:
          "https://drive.google.com/uc?export=view&id=1PFl6xkPjJM8SajaPz6FyaVFn0zZYp4i9",
        text:
          "イベント作成者はコミュニティがどのようなイベントを求めているのかが確認できます。"
      }
    ]
  }),
  mounted() {
    setInterval(() => {
      this.mediaQuery = matchMedia("(max-width: 1400px)").matches; // eslint-disable-line
    }, 500);
  }
};
</script>

<style scoped>
.login-form {
  border-radius: 20px 20px 20px 20px;
  background-color: rgba(255, 255, 255, 0.8);
  height: 350px;
  box-shadow: 2px 2px 4px gray;
}
.cube {
  animation: cube 3s linear infinite;
  transform-origin: 50% 50%;
  margin: 1rem 0 !important;
}

@keyframes cube {
  0% {
    transform: translateY(0);
  }
  33.33333% {
    transform: translateY(-10px);
  }
  66.66667% {
    transform: translateY(0);
  }
  100% {
    transform: translateY(0);
  }
}

@media screen and (max-width: 1400px) {
  .flex-parallax {
    height: 1000px;
  }
  .parallax {
    height: 100%;
    width: auto;
  }
}
</style>>