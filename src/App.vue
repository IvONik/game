<template>
  <div id="app">
    <Game/>
    <!-- <SudokuComp/> -->
  </div>
</template>

<script>
import Game from './components/Game.vue'
import SudokuComp from './components/SudokuComp.vue'

export default {
  name: 'App',
  components: {
    Game,
    SudokuComp,
    // MortgageCalcComp,
  }
}
</script>

<style>
#app {
  font-family: 'Roboto', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body {
  font-family: "Roboto", sans-serif;
  font-weight: 400;
  font-style: normal;
}
</style>
