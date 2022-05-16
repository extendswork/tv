<script>
    import { onMount } from "svelte/internal";
    import Hls from "hls.js";
  
    export let src;
    export let poster;
    let cls;
    export {cls as class};
    onMount(() => {
      let player = document.querySelector("#player");
  
      if (Hls.isSupported()) {
        const hls = new Hls();
        hls.loadSource(src);
        hls.attachMedia(player);
        hls.on(Hls.Events.MEDIA_ATTACHED, function () {
          video.play();
        });
      }
    });
  </script>
  
  <!-- svelte-ignore a11y-media-has-caption -->
  <video id="player" class="{cls} w-full h-full" {poster} controls></video>