<template>
  <div>
    <h1>Vuejs Hlsjs</h1>

    <video id="video" controls webkit-playsinline autoplay muted></video>
    <button @click="PlayVide()">動画を再生する</button>

    <img src="../src/assets/logo.png" alt="image" class="img" />
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
        hls.loadSource("../src/assets/video/1080_out.m3u8");
        hls.attachMedia(video);
        hls.on(Hls.Events.MANIFEST_PARSED, function() {
          video.play();
        });
      }
    }
  }
};
</script>

<style>
.img {
  background-image: url("../src/assets/logo.png");
}

#video {
  height: 300px;
}
</style>
