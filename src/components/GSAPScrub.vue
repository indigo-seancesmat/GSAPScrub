<template>
  <div class="gsap-scrub" :style="{ minHeight: `${minHeight}px` }">
    <canvas ref="canvas" />
  </div>
</template>

<script>
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
gsap.registerPlugin(ScrollTrigger);

export default {
  name: "GSAPScrub",
  props: {
    sequence: {
      type: String,
      default: "pinkandblue"
    },
    frameCount: Number,
    minHeight: {
      type: Number,
      default: 4000
    }
  },
  mounted() {
    const canvas = this.$refs.canvas;
    const context = canvas.getContext("2d");

    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    // const frameCount = 27;
    const currentFrame = (index) =>
      `/kuma/${this.sequence}/kuma_${this.sequence +
        (index + 1).toString()}.jpg`;

    const images = [];
    const kuma = {
      frame: 0
    };

    for (let i = 0; i < this.frameCount; i++) {
      const img = new Image();
      img.src = currentFrame(i);
      images.push(img);
    }

    gsap.to(kuma, {
      frame: this.frameCount - 1,
      snap: "frame",
      scrollTrigger: {
        scrub: 0.5
      },
      onUpdate: render // use animation onUpdate instead of scrollTrigger's onUpdate
    });
    window.scrollTo(0, 0);

    images[0].onload = render;

    function render() {
      context.clearRect(0, 0, canvas.width, canvas.height);
      console.log(images[kuma.frame]);
      if ((2176 / 3840) * canvas.width < canvas.height) {
        let newWidth = (3840 / 2176) * canvas.height;
        let newHeight = canvas.height;
        context.drawImage(
          images[kuma.frame],
          (canvas.width - newWidth) / 2,
          0,
          newWidth,
          newHeight
        );
      } else {
        let newWidth = canvas.width;
        let newHeight = (2176 / 3840) * canvas.width;
        context.drawImage(
          images[kuma.frame],
          0,
          (canvas.height - newHeight) / 2,
          newWidth,
          newHeight
        );
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
canvas {
  position: fixed;
  /* left: 50%;
  top: 50%;
  transform: translate(-50%, -50%); */
  width: 100vw;
  height: 100vh;
  top: 0;
  left: 0;
}
.gsap-scrub {
  position: absolute;
  width: 100vw;
}
</style>
