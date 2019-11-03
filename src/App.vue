<template>
  <div id="app">
    <app-canvas></app-canvas>
  </div>
</template>

<script>
import AppCanvas from './components/Canvas.vue';

export default {
  name: 'app',
  components: {
    AppCanvas,
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
}

#app {
  width: 100vw;
  height: 100vh;
  padding: 10px;
}

.container {
  position: relative;
  width: 100%;
  height: 100%;
}

.canvas {
  position: relative;
  width: 100%;
  height: 100%;
  border: 2px solid #000;
}

.settings-panel {
  position: absolute;
  top: 0;
  left: 0;
  border: 1px solid #000;
}
</style>
