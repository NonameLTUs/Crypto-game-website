<template>
  <div id="app">
    <Game />
  </div>
</template>

<script>
  import Game from './Game'

  export default {
    name: 'App',
    components: {
      Game
    }
  }

</script>

<style>
  #app {
    font-family: 'Raleway', sans-serif;
    color: #4f3b8e;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
</style>