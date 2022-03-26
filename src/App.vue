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
@font-face {
  font-family: "Hind";
  src: url("./font/Hind-Light.ttf");
}

* {
  font-family: "Hind", monospace;      
}


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
  background: linear-gradient(to right, rgb(96, 108, 136), rgb(63, 76, 107));
}
</style>
