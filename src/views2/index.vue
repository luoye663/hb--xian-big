<template>
  <div id="index">
    <dv-full-screen-container class="bg">
      <dv-loading v-if="loading">Loading...</dv-loading>
      <div v-else class="host-body">
        <div class="d-flex jc-center">
          <dv-decoration-10 style="width:33.3%;height:.0625rem;"/>
          <div class="d-flex jc-center">
            <dv-decoration-8 :color="['#568aea', '#000000']" style="width:2.5rem;height:.625rem;"/>
            <div class="title">
              <span class="title-text" style="font-size: 20px">软通项目智慧工地平台</span>

              <dv-decoration-6--  >
<!--                <span class="title-text">软通项目智慧工地平台</span>-->
              </dv-decoration-6-->
<!--              <dv-decoration-6-->
<!--                  class="title-bototm"-->
<!--                  :reverse="true"-->
<!--                  :color="['#50e3c2', '#67a1e5']"-->
<!--                  style="width:3.125rem;height:.1rem;"-->
<!--              />-->
            </div>
            <dv-decoration-8
                :reverse="true"
                :color="['#568aea', '#000000']"
                style="width:2.5rem;height:.625rem;"
            />
          </div>
          <dv-decoration-10 style="width:33.3%;height:.0625rem; transform: rotateY(180deg);"/>
        </div>

        <!-- 第二行 -->
        <div class="dv-border-box-5 d-flex jc-between px-2">

          <div class="d-flex" style="width: 40%">
            <dv-border-box-8 class="react-right ml-4" style=" text-align: center;">
              <!--              <span class="react-before "></span>-->
              <span class="text fw-b home-font-size" @click="handelClick('home')">首页</span>
            </dv-border-box-8>


            <dv-border-box-8 class="react-right ml-3 ">
              <span class="text fw-b home-font-size" @click="handelClick('video')">视频监控</span>
            </dv-border-box-8>

<!--            <dv-border-box-8 class="react-right ml-3 ">
              <span class="text fw-b home-font-size" @click="handelClick('positioning')">环境监测</span>
            </dv-border-box-8>-->
          </div>


          <div style="width: 40%;" class="d-flex">

            <!--:style="styleActive.towerCrane"
                @mouseenter="enters('towerCrane')"
                @mouseleave="leaver('towerCrane')"-->

            <dv-border-box-8 class="react-left mr-4" style="margin-left: 0.35rem">
              <span class="text fw-b home-font-size" @click="handelClick('towerCrane')">塔群监测</span>
            </dv-border-box-8>
            <!--视频监控-->
            <dv-border-box-8 class="react-left mr-3">
              <!--/*             <span class="react-after" style="background: #1a5cd7"></span>*/-->
              <span class="text fw-b home-font-size" @click="handelClick('environment')">定位监测</span>
            </dv-border-box-8>
            <!-- 时间-->
            <dv-border-box-8 class="react-left mr-4">
              <!--/*             <span class="react-after" style="background: #1a5cd7"></span>*/-->
              <span class="text fw-b home-font-size">{{ dateYear }} {{ dateWeek }} {{ dateDay }}</span>
            </dv-border-box-8>

          </div>
        </div>


      </div>
      <div style="height: 100%;margin-top: 0.2rem;margin-left: 0.1rem; margin-right:0.1rem;width: 100%">
        <iframe id="ifra" :src="iframe_url" frameborder="0" style="width: 100%;height: 100%"></iframe>
      </div>

    </dv-full-screen-container>
  </div>
</template>

<script>
import {formatTime} from '../utils/index.js'
// import centerLeft1 from "./centerLeft1";
// import centerLeft2 from "./centerLeft2";
// import centerRight1 from "./centerRight1";
// import centerRight2 from "./centerRight2";
// import center from "./center";
// import bottomLeft from "./bottomLeft";
// import bottomRight from "./bottomRight";
export default {
  data() {
    return {
      loading: true,
      dateDay: null,
      dateYear: null,
      dateWeek: null,
      weekday: ["周日", "周一", "周二", "周三", "周四", "周五", "周六"],
      iframe_url: '',
      styleActive: {}
    };
  },
  components: {
    // centerLeft1,
    // centerLeft2,
    // centerRight1,
    // centerRight2,
    // center,
    // bottomLeft,
    // bottomRight
  },
  mounted() {
    this.timeFn();
    this.cancelLoading();
    var _this = this;
    var iframe = document.querySelector("#ifra");
    // 处理兼容行问题
    if (iframe.attachEvent) {
      iframe.attachEvent('onload', function () {
        // iframe加载完毕以后执行操作
        console.log('iframe已加载完毕')
        _this.loading = false;
      })
    } else {
      iframe.onload = function () {
        // iframe加载完毕以后执行操作
        console.log('iframe已加载完毕')
        _this.loading = false;
      }
    }

  },
  methods: {
    timeFn() {
      setInterval(() => {
        this.dateDay = formatTime(new Date(), 'HH: mm: ss');
        this.dateYear = formatTime(new Date(), 'yyyy-MM-dd');
        this.dateWeek = this.weekday[new Date().getDay()];
      }, 1000)
    },
    cancelLoading() {
      setTimeout(() => {
        this.loading = false;
      }, 500);
    },
    handelClick(type) {
      switch (type) {
        case 'video':
          this.iframe_url = 'http://127.0.0.1:8881/html2/';
          break;
        case 'positioning':
          console.log("positioning")
          this.iframe_url = 'https://www.baidu.com';
          break;
        case 'towerCrane':
          this.iframe_url = 'https://tieba.baidu.com';
          break;
        case 'environment':
          this.iframe_url = 'https://www.cnblogs.com/wxcbg/p/5908967.html';
          break;
      }
    },
    enters(index) {
      switch (index) {
        case 'towerCrane':
          this.styleActive.towerCrane = 'background: #1a5cd7';
          break;
        case 'positioning':
          console.log("positioning")
          this.iframe_url = 'https://www.baidu.com';
          break;
        case 'towerCrane1':
          this.iframe_url = 'https://tieba.baidu.com';
          break;
        case 'environment':
          this.iframe_url = 'https://www.cnblogs.com/wxcbg/p/5908967.html';
          break;
      }/**/
    },
    leaver(index) {
      switch (index) {
        case 'home':
          this.iframe_url = 'https://bing.com';
          break;
        case 'positioning':
          console.log("positioning")
          this.iframe_url = 'https://www.baidu.com';
          break;
        case 'towerCrane':
          this.styleActive.towerCrane = '';
          break;
        case 'environment':
          this.iframe_url = 'https://www.cnblogs.com/wxcbg/p/5908967.html';
          break;
      }
    }
  }
};
</script>

<style lang="scss">
@import '../assets/scss/index.scss';

.home-font-size {
  font-size: large
}
</style>
