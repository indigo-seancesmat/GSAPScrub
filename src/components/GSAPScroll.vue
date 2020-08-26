<template>
  <div class="gsap-scroll">
    <div class="gsap-scroll__box"></div>
  </div>
</template>

<script>
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
gsap.registerPlugin(ScrollTrigger);
export default {
  name: "GSAPScroll",
  mounted() {
    gsap.to(".gsap-scroll__box", {
      scrollTrigger: {
        trigger: ".gsap-scroll__box",
        start: "bottom center",
        end: "top top",
        scrub: true,
        markers: { startColor: "green", endColor: "red", fontSize: "12px" }
      },
      x: 500,
      scale: 0
    });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.gsap-scroll {
  position: absolute;
  width: 100vw;
  min-height: 100vh;
}
.gsap-scroll__box {
  background: rebeccapurple;
  margin-top: 100vh;
  margin-bottom: 100vh;
  width: 200px;
  height: 200px;
}
</style>
