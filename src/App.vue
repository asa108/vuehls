<template>
  <div>
    <h1>Vuejs Hlsjs</h1>

    <video ref="video" id="video" controls webkit-playsinline muted></video>
    <button @click="PlayVide()">動画を再生する</button>
    <button @click="changeResolution(3)">lecel3を再生</button>

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
        // hls.loadSource(
        //   "https://bitdash-a.akamaihd.net/content/MI201109210084_1/m3u8s/f08e80da-bf1d-4e3d-8899-f0f6155f6efa.m3u8"
        // );
        hls.loadSource("./video/playlist.m3u8");
        hls.attachMedia(video);
        hls.on(Hls.Events.MANIFEST_PARSED, function(event, data) {
          console.log(event); //hlsManifestParsed
          console.log(
            "manifest loaded, found " + data.levels.length + " quality level"
          );
          console.log(data.levels); // 6
          console.log(data);
          hls.currentLevel();
          hls.autoLevelEnabled = false;
          hls.currentLevel = 3;
          video.play();
        });
        // hls.on(Hls.Events.MANIFEST_PARSED, function() {
        //   video.play();
        // });
      }
    }
    // changeResolution() {
    //   var video = document.getElementById("video");
    //   var hls = new Hls();

    //   console.log(n);
    //   hls.currentLevel = n;

    //   setTimeout(() => {
    //     console.log(hls.nextLevel);
    //   }, 1000);
    // }
  }
};
</script>

<style>
.img {
  /* background-image: url("../src/assets/logo.png"); */
}

#video {
  height: 300px;
}
</style>
