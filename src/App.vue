<template>
  <div id="app">
    <div class="nav">
      <button
        @click="setBackground('pinkandblue', 61)"
        :class="{ nav__current: seq === 'pinkandblue' }"
      >
        Pink & Blue
      </button>
      <button
        @click="setBackground('green', 81)"
        :class="{ nav__current: seq === 'green' }"
      >
        Green
      </button>
      <button
        @click="setBackground('pinkandteal', 58, 3000)"
        :class="{ nav__current: seq === 'pinkandteal' }"
      >
        Pink & Teal
      </button>
    </div>
    <GSAPScrub
      :sequence="seq"
      :frame-count="frames"
      :min-height="minHeight"
      :key="seq"
    />
  </div>
</template>

<script>
import GSAPScrub from "./components/GSAPScrub";

export default {
  name: "App",
  components: {
    GSAPScrub
  },
  data() {
    return {
      seq: "pinkandblue",
      frames: 61,
      minHeight: 4000
    };
  },
  methods: {
    setBackground(seq, frames, minHeight = 3000) {
      this.seq = seq;
      this.frames = frames;
      this.minHeight = minHeight;
    }
  }
};
</script>

<style>
html,
body {
  margin: 0;
  padding: 0;
  overscroll-behavior: none;
  overflow-x: hidden;
}
/* b  */
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.nav {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 1000;
  height: 40px;
  background: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(10px);
  display: flex;
  justify-content: center;
}
.nav * {
  align-self: center;
}
.nav button {
  margin: 0 4px;
  cursor: pointer;
  border: none;
  padding: 4px 12px;
  background: #e1e1e1;
  font-weight: bold;
}
.nav button:hover,
.nav button:active {
  background: #94fff7;
}
.nav button.nav__current {
  background: #94fff7;
}
</style>
