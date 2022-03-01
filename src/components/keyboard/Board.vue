<template>
  <div>
    <div class="keyboard">
      <div v-for="(item, index) in keyboard.lvl1" :key="index">
        <Key :label="item" @click.native="matchWord(item)"/>
      </div>
    </div>
    <div class="keyboard">
      <div v-for="(item, index) in keyboard.lvl2" :key="index">
        <Key :label="item" @click.native="matchWord(item)"/>
      </div>
    </div>
    <div class="keyboard">
      <div v-for="(item, index) in keyboard.lvl3" :key="index">
        <Key :label="item" @click.native="matchWord(item)"/>
      </div>
    </div>
  </div>
</template>

<script>
import Key from "./Key.vue";

export default {
  components: {    
    Key
  },

  data() {
    return {      
      keyboard: {
        lvl1: ['q', 'w', 'e', 'r', 't', 'y', 'u', 'i', 'o', 'p'],
        lvl2: ['a', 's', 'd', 'f', 'g', 'h', 'j', 'k', 'l'],
        lvl3: ['z', 'x', 'c', 'v', 'b', 'n', 'm']
      }
    };
  },

  methods: {
    matchWord(n) {
      this.$parent.matchWord(n);
    }
  }
};
</script>

<style scoped>
.keyboard {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>