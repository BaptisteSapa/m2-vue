<template>
  <div id="app">
    <Moon />
    <transition-group name="fade">
      <Star v-for="(star, index) in stars"
        :key="index"
        :style="`top: ${star.y}px; left: ${star.x}px;`"/>
    </transition-group>
    <input 
      type="range"
      name="stars" 
      min="10"
      max="600"
      v-model.number="nbStars"
    />
  </div>
</template>

<script>
import { randomX, randomY } from "./helpers/random";
import Moon from "./components/Moon";
import Star from "./components/Star";

export default {
  name: "app",
  computed: {
    stars() {
      const nbStars = 100;
      const arrStars = [];
      for (let index = 0; index < nbStars; index++) {
        arrStars.push({
          x: randomX(),
          y: randomY()
        });
      }
      return arrStars;
    }
  },
  components: {
    Moon,
    Star
  }
};
</script>

<style lang="scss">
body {
  margin: 0;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100vh;
  width: 100vw;
  background: radial-gradient(ellipse at bottom, #1b2735 0%, #090a0f 100%);
}

/* Transitions */

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
