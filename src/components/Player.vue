<!--
 * @Author: HuBotao
 * @Date: 2020-10-29 09:51:11
 * @LastEditTime: 2020-11-18 10:11:05
 * @LastEditors: HuBotao
 * @Description:
-->

<template>
  <div>
    <video
      ref="video"
      controls
      class="video-js vjs-default-skin vjs-big-play-centered"
    ></video>
  </div>
</template>

<script>
export default {
  name: "Player",
  data() {
    return {
      player: null,
      // options: {},
      // /
    };
  },
  props: {
    options: {
      type: Object,
      default: function () {
        return {
          playbackRates: [0.1, 0.2, 0.5, 1.0], //播放速度
          controls: true,
          autoplay: true, //如果true,浏览器准备好时开始播放。
          muted: false, // 默认情况下将会消除任何音频。
          loop: true, // 导致视频一结束就重新开始。
          preload: "auto", // auto浏览器选择最佳行为,立即开始加载视频（如果浏览器支持）
          language: "zh-CN",
          aspectRatio: "16:9", // 播放器的比例。用冒号分隔的两个数字（例如"16:9"或"4:3"）
          fluid: true, // 当true时，播放器将拥有流体大小。换句话说，它将按比例缩放以适应其容器。
          sources: [
            {
              type: "",
              src: " ", //url地址
            },
          ],
          poster: "", //你的封面地址
          width: "800px",
          height: "200px",
          notSupportedMessage: "此视频暂无法播放，请稍后再试", //无法播放媒体源时显示的默认信息。
          controlBar: {
            playToggle: true,
            timeDivider: true,
            durationDisplay: true,
            remainingTimeDisplay: false,
            fullscreenToggle: true, //全屏按钮
          },
          errorDisplay: true,
          posterImage: false,
          bigPlayButton: true,
          textTrackDisplay: true,
        };
      },
    },
    sources: {
      type: Object,
      default: function () {
        return {
          type: "video/mp4",
          src: "https://upos-sz-mirrorks3.bilivideo.com/upgcxcode/90/90/109149090/109149090-1-208.mp4?e=ig8euxZM2rNcNbKV7bdVhwdl7wdjhwdVhoNvNC8BqJIzNbfq9rVEuxTEnE8L5F6VnEsSTx0vkX8fqJeYTj_lta53NCM=&uipk=5&nbs=1&deadline=1612172159&gen=playurl&os=ks3bv&oi=978800370&trid=5b2532c559a0465ea475d6b593e2b865T&platform=html5&upsig=5ea5b3963b8121c4f8120c0ed693b2d3&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,platform&mid=524602686&orderid=0,1&logo=80000000",
        };
      },
    },
  },
  watch: {
    src() {
      this.player.src(this.src);
    },
    sources: function () {},
  },
  computed: {
    src() {
      return this.options.sources[0].src;
    },
  },
  mounted() {
    const vm = this;
    this.player = this.$video(this.$refs.video, this.options);
  },
  beforeMount() {
    this.$set(this.options.sources, 0, this.sources);
  },
};
</script>


<style>
.vjs-big-play-button {
  height: 3em !important;
  width: 3em !important;
  line-height: 3em !important;
  border-radius: 50% !important;
}

.vjs-button > .vjs-icon-placeholder:before {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 2em;
}

.vjs-slider-horizontal .vjs-volume-level:before {
  top: -0.333333333333333em;
  right: -0.5em;
}

.vjs-playback-rate .vjs-playback-rate-value {
  font-size: 1.8em;
  display: flex;
  align-items: center;
  justify-content: center;
}

.vjs-control-bar {
  background: rgba(0, 0, 0, 0.8) !important;
}

.video-js .vjs-play-progress,
.video-js .vjs-volume-level {
  background: linear-gradient(to right, #ff7b02, #ffa604) !important;
}

.video-js:hover .vjs-big-play-button,
.vjs-custom-skin > .video-js .vjs-big-play-button:focus,
.vjs-custom-skin > .video-js .vjs-big-play-button:active {
  background: linear-gradient(to right, #ff7b02, #ffa604) !important;
  opacity: 0.7;
}

.vjs-big-play-button .vjs-icon-placeholder {
  font-size: 70px !important;
}

.vjs-error .vjs-error-display:before {
  color: #fff !important;
  content: "X" !important;
  font-family: Arial, Helvetica, sans-serif !important;
  font-size: 4.5em !important;
  left: 0 !important;
  line-height: 1.8 !important;
  margin-top: -0.5em !important;
  position: absolute !important;
  text-shadow: 0.05em 0.05em 0.1em #000 !important;
  text-align: center !important;
  top: 50% !important;
  vertical-align: middle !important;
  width: 100% !important;
}
</style>
