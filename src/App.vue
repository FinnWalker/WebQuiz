<template>
  <div id="app">
    <Home />
  </div>
</template>

<script>
import Home from './components/Home';
export default {
  name: 'app',
  components: {
    Home
  }
}
</script>

<style>
body {
  margin: 0;
  background: black;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  width: 100vw;
  height: 56.25vw;
  background: url('./assets/img/stars.png');
  background-size: cover;
  position: absolute;
  left: 0;
  right: 0;
  margin: auto;
}

@media (min-aspect-ratio: 16/9)  {
  #app {
    height: 100vh;
    width: 177.777777778vh;
  }
}
</style>
