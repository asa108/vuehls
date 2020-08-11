<template>
  <div id="app">
    <!-- <p>{{msg}}</p> -->
    <video
      ref="video"
      id="video"
      style="width: 800px; height: 600px;"
      controls
      muted
      playsinline
      autoplay
    >
      <!-- <source src="/src/assets/video/1080_out.m3u8" /> -->
      <!-- type='application/x-mpegURL' -->
    </video>
    <button v-on:click="playVideo">play</button>
  </div>
</template>

<script>
// import hlsjs from ""; // hlsjsをnpmでインストール
import Hls from "hls.js";

// var video_url = ;

export default {
  data: () => {
    return {
      // hlsjsを機能させるための初期化処理を格納した変数
      hls: new Hls()
    };
  },
  methods: {
    // 動画再生時にこの関数を叩く
    playVideo: function('/src/assets/video/1080_out.m3u8') {
      // this.$nextTick(function() {
      // var video = $(this.refs["video"]).get(0);
      if (Hls.isSupported('/src/assets/video/1080_out.m3u8')) {
        var hls = this.hls;
        hls.loadSource();
        hls.attachMedia(this.refs["video"]);
        hls.on(Hls.Events.MANIFEST_PARSED, function() {
          // 動画再生
          this.refs["video"].play();
        });
      }
      // else if (
      //   this.refs["video"].canPlayType("application/vnd.apple.mpegurl")
      // ) {
      //   this.refs["video"].src = video_url;
      //   this.refs["video"].addEventListener("loadedmetadata", function() {
      //     // 動画再生
      //     this.refs["video"].play();
      //   });
      // }
      // });

    // }

    // 動画停止時にこの関数を叩く
    // stopVideo: function() {
    //   // 動画停止
    //   this.hls.destroy();
    // }
  }
};

// export default {
//   data() {
//     return {
//       msg: "Hello World!"
//     };
//   }
// };
</script>

<style></style>
