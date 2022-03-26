<template>
  <div class="hangman">
    <h1>{{attempts}}</h1>
    <div class="letters">
      <div v-for="(item, index) in word" :key="index">
        <div class="letters">
          <Letter v-if="item.visible" :letter="item.letter" />
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


    <div class="letters">
      <div v-for="(item, index) in word" :key="index">
        <Letter v-show="attempts == 0" :letter="item.letter"/>
      </div>
    </div>    
  </div>
</template>

<script>
import { words } from "./words.js"
import Letter from "./Letter.vue";
import Board from "./keyboard/Board.vue";

export default {
  components: {
    Letter,
    Board
  },  

  data() {
    return {
      attempts: 10,
      completed: false,
      word: [],
      usedWord: []
    };
  },  

  mounted() {
    //Check if the word match with keyboard
    window.addEventListener('keypress', e => {        
        let a = e.key.toLowerCase();

        if(this.attempts > 0 && !this.usedWord.includes(a) && !this.completed) {          
          let obj = this.word.filter((obj => obj.normLetter === a))
          
          if(obj == 0) {
            this.attempts--;
            this.usedWord.push(a);
          } else {
            for(var i = 0; i < obj.length; i++) {
              this.word[obj[i].id].visible = true;
            }
          }           
        }
        //Check if player won the game
        this.completed = this.word.every(elem => elem.visible == true);
      });
    
  },

  methods: {
    initialState() {
      return {
        attempts: 10,
        completed: false,
        word: [],
        usedWord: []
      }
    },

    resetData() {
      Object.assign(this.$data, this.initialState());
    },

    chooseWord() {      
      var word = words[Math.floor(Math.random() * words.length)];
      var normalizedWord = word.normalize("NFD").replace(/[\u0300-\u036f]/g, "")

      this.resetData();      
      
      for(var j = 0; j < word.length; j++) {
        if(word[j] !== '') {
          var obj = {
            letter: word[j], 
            normLetter: normalizedWord[j],
            visible: false, 
            id: j};
          this.word.push(obj);
        }
      }
    },

    matchWord(n) {      
      //Check if the word match with board
      if(this.attempts > 0 && !this.usedWord.includes(n) && !this.completed) {
        let obj = this.word.filter((obj => obj.normLetter === n))              

        if(obj == 0) {
          this.attempts--;
          this.usedWord.push(n);
        } else {
          for(var i = 0; i < obj.length; i++) {
            this.word[obj[i].id].visible = true;
          }
        }
      }
      //Check if player won the game
      this.completed = this.word.every(elem => elem.visible == true);
    },        
  }
};
</script>

<style scoped>
.letters {  
  height: 35px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.bd {
  border-bottom: 5px solid black;
  width: 40px;
  margin: 5px;
  margin-bottom: 15px;
  margin-top: 0px;
}
</style>