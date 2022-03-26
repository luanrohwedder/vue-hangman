<template>
  <div class="label" @click="$emit('onclick', label)">
    <div> {{ label }} </div>    
  </div>
</template>

<script>
export default {
  props: {
    label: {},
    hit: { type: Boolean},
    status: {
      hit: false,
      miss: false
    }
  }  
};
</script>

<style scoped>
.label {
  height: 40px;
  width: 40px;
  color: white;
  background-color: rgba(0, 0, 0, 0.4);
  user-select: none;
  font-size: 1.5em;
  margin: 5px;
  border-radius: 10px;
}
</style>
