<template>
  <div id="app">
    <GSAPScrub/>
  </div>
</template>

<script>
import GSAPScrub from "./components/GSAPScrub";

export default {
  name: "App",
  components: {
    GSAPScrub
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
