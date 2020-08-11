<template>
  <div>
    <h1>Vuejs Hlsjs</h1>

    <video
      ref="video"
      id="video"
      controls
      webkit-playsinline
      muted
      autoplay
    ></video>
    <button @click="PlayVide()">動画を再生する</button>
    <button @click="changeResolution(4)">level4を再生</button>
    <button @click="changeResolution(0)">level1を再生</button>

    <img src="../public/logo.png" alt="image" class="img" />
    <!-- <img src="./assets/Icon_3d.png" alt="" /> -->
  </div>
</template>

<script>
import Hls from "hls.js";

export default {
  data() {
    return {
      hls: new Hls()
    };
  },
  methods: {
    PlayVide() {
      var video = document.getElementById("video");
      if (Hls.isSupported()) {
        var hls = new Hls();
        // hls.currentLevel = n;
        // hls.loadSource(
        //   "https://bitdash-a.akamaihd.net/content/MI201109210084_1/m3u8s/f08e80da-bf1d-4e3d-8899-f0f6155f6efa.m3u8"
        // );
        hls.loadSource("./video/playlist.m3u8");
        hls.attachMedia(video);
        hls.on(Hls.Events.MANIFEST_PARSED, function(event, data) {
          console.log(data.levels);
          hls.currentLevel();
          // hls.autoLevelEnabled = false;
          // hls.currentLevel = 3;
          video.play();
        });
      }
    },
    changeResolution(n) {
      //ボタンにある引数を取ってきてそれをhls.currentLevelに代入することで
      //解像度が変わる
      //引数は取れてきてるけど、hls.currentLevelに入れれてない
      var hls = new Hls();
      hls.currentLevel = n;

      console.log(n); //引数の値表示、1 or 4
      setTimeout(() => {
        console.log(hls.currentLevel);
      }, 1000);
    }
  }
};
</script>

<style>
#video {
  height: 300px;
}
</style>
