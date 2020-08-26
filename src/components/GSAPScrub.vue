<template>
  <div class="gsap-scroll">
    <canvas ref="canvas"/>
  </div>
</template>

<script>
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
gsap.registerPlugin(ScrollTrigger);
export default {
  name: "GSAPScrub",
  mounted() {
    const canvas = this.$refs.canvas;
    const context = canvas.getContext("2d");

    canvas.width = 1158;
    canvas.height = 770;

    const frameCount = 27;
    const currentFrame = index =>
      `~/assets/scrub/kuma000${(index + 1).toString().padStart(4, "0")}.jpg`;

    const images = [];
    const kuma = {
      frame: 0
    };

    for (let i = 0; i < frameCount; i++) {
      const img = new Image();
      img.src = currentFrame(i);
      images.push(img);
    }

    gsap.to(kuma, {
      frame: frameCount - 1,
      snap: "frame",
      scrollTrigger: {
        scrub: 0.5
      },
      onUpdate: render // use animation onUpdate instead of scrollTrigger's onUpdate
    });

    images[0].onload = render;

    function render() {
      context.clearRect(0, 0, canvas.width, canvas.height);
      console.log(images[kuma.frame]);
      // context.drawImage(images[kuma.frame], 0, 0);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
canvas {
  position: fixed;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  max-width: 100vw;
  max-height: 100vh;
}
.gsap-scroll {
  position: absolute;
  width: 100vw;
  min-height: 5000px;
}
</style>
