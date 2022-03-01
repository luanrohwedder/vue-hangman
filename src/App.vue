<template>
  <div id="app">
    <h1>Jogo da Forca</h1>
    <Hangman/>
  </div>
</template>

<script>
import Hangman from './components/Hangman.vue'

export default {
  name: 'App',
  components: {
    Hangman
  }
}
</script>

<style>
body {
  margin: 0;
}

#app {
  display: flex;
  flex-direction: column;
  height: 100vh;
  justify-content: center;
  align-items: center;
  text-align: center;
  color: rgb(211, 211, 211);
  background: linear-gradient(to right, rgb(97, 97, 97), rgb(155, 197, 195));
}
</style>
