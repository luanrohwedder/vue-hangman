<template>
  <div class="hangman">
    <h1>Tentativas: {{attempts}}</h1>
    <div class="letters">
      <div v-for="(item, index) in word" :key="index">
        <div v-if="item.visible">
          <Letter :letter="item.letter" />
        </div>
        <p class="bd"></p>
      </div>
    </div>
    <button v-on:click="chooseWord">start</button>
    
    <Board/>

    <div class="letters">
      <div v-for="(item, index) in usedWord" :key="index">
        <Letter :letter="item" usedWord/>
      </div>
    </div>
  </div>
</template>

<script>
import Letter from "./Letter.vue";
import Board from "./keyboard/Board.vue";

export default {
  components: {
    Letter,
    Board
  },

  data() {
    return {
      attempts: 6,
      word: [],
      usedWord: [],
      words: ["teclado", "computador", "mouse"],
      keyboard: {
        lvl1: ['q', 'w', 'e', 'r', 't', 'y', 'u', 'i', 'o', 'p'],
        lvl2: ['a', 's', 'd', 'f', 'g', 'h', 'j', 'k', 'l'],
        lvl3: ['z', 'x', 'c', 'v', 'b', 'n', 'm']
      }
    };
  },  

  mounted() {
    window.addEventListener('keypress', e => {        
        let a = String.fromCharCode(e.keyCode).toLowerCase();

        if(this.attempts > 0 && !this.usedWord.includes(a)) {          
          let obj = this.word.filter((obj => obj.letter === a))
          
          if(obj == 0) {
            this.attempts--;
            this.usedWord.push(a);
          } else {
            for(var i = 0; i < obj.length; i++) {
              this.word[obj[i].id].visible = true;
            }
          }
        }
      });    
  },

  created() {
    this.chooseWord();
  },

  methods: {
    chooseWord() {
      var i = Math.floor(Math.random() * 3);
      var word = this.words[i];
      
      //Reset data
      this.word = [];
      this.attempts = 6;
      this.usedWord = [];      
      
      for(var j = 0; j < word.length; j++) {
        if(word[j] !== '') {
          var obj = {letter: word[j], visible: false, id: j};          
          this.word.push(obj);
        }

      }
    },

    matchWord(n) {
      if(this.attempts > 0 && !this.usedWord.includes(n)) {
        let obj = this.word.filter((obj => obj.letter === n))              

        if(obj == 0) {
          this.attempts--;
          this.usedWord.push(n);
        } else {
          for(var i = 0; i < obj.length; i++) {
            this.word[obj[i].id].visible = true;
          }
        }
      }
    }
  }
};
</script>

<style scoped>
.letters {
  display: flex;
  justify-content: center;
  align-items: center;
}

.bd {
  border-bottom: 5px solid black;
  width: 40px;
  margin: 5px;
}
</style>