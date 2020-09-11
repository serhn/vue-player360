<template>
  <div>
    <VueRoundslider
      :duration="duration"
      :position="position"
      :diametr="300"
      :widthCircle="10"
      :colorLine="colorLine"
      :onPosition="sliderEventPosition"
      :onMouseMoveCenter="sliderEventMouseMoveCenter"
      :onMouseClickCenter="sliderEventMouseClickCenter"
      :onMouseMovePosition="sliderEventMouseMovePosition"
    >
      <Play v-if="playStatus==='STOPPED'"></Play>
      <Stop v-if="mouseMoveCenter && playStatus==='PLAYING'"></Stop>
      <Waiting v-if="loading"></Waiting>
    </VueRoundslider>
    <VueSoundmanager
      :onPlaying="soundEventPlaying"
      :url="url"
      :randUrl="randUrl"
      :position="playFromPosition"
      :playStatus="playStatus"
    ></VueSoundmanager>
  </div>
</template>

<script>
import VueSoundmanager from "/Users/serh/doc/projects/vue-soundmanager/src/vue-soundmanager.vue";
import VueRoundslider from "@serh/vue-roundslider";


//const COLOR_LINE_DEFAULT = "green";
//const COLOR_LINE_END = "blue";
export default {
  components: {
    VueRoundslider,
    VueSoundmanager,
    Play,
    Stop,
    Waiting,
  },
  props: {
    url: {
      type: String,
      required: true,
    },
    colorLine: {
      type: String,
      default: "green",
    },
    randUrl: {
      type: Boolean,
      default: false,
    },
  },
  data: () => ({
    duration: 0,
    position: 0,
    timerInterval: null,
    mouseMoveCenter: false,
    playFromPosition: 0,
    loading: false,
    playStatus: "STOPPED",
  }),
  watch: {
    position: function (val) {
      if (val >= this.duration) {
        this.playStatus="STOPPED"
      }
    },
    mouseMoveCenter: function (val) {
      if (val === true) {
        console.log("Mouse over center");
      } else {
        console.log("Mouse out center");
      }
    },
  },
  mounted() {},

  methods: {
    sliderEventPosition(position) {
      this.playFromPosition = position;
      console.log(position);
    },
    sliderEventMouseMoveCenter(event) {
      this.mouseMoveCenter = true;
    },
    sliderEventMouseMovePosition(event) {
      this.mouseMoveCenter = false;
    },
    sliderEventMouseClickCenter(event) {
      if (this.playStatus == "PLAYING") {
        this.playStatus = "STOPPED";
      } else {
        this.playStatus = "PLAYING";
      }
    },

    soundEventPlaying(player) {
      this.duration = Math.ceil(player.duration / 1000);
      this.position = Math.ceil(player.position / 1000);
    },
  },
};
</script> 
 
<style scoped lang="scss">
</style> 