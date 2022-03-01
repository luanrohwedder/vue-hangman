<template>
  <div class="letter" :class="{usedWord}">
    <h3> {{ letter }} </h3>
  </div>
</template>

<script>
export default {
  props: {
    letter: {},
    usedWord: { type: Boolean }
  }
};
</script>

<style scoped>
.letter {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 20px;  
  width: 40px;
  color: white;
  user-select: none;  ;
  font-size: 1.2em;
  margin: 5px;
}

.letter.usedWord {
  margin-top: 20px;
  color: black;
}
</style>
