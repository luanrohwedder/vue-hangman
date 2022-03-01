<template>
  <div class="label" @click="$emit('onclick', label)">
    {{ label }} 
  </div>
</template>

<script>
export default {
  props: {
    label: {}
  }
};
</script>

<style scoped>
.label {
  height: 40px;
  width: 40px;
  color: white;
  background-color: brown;
  user-select: none;
  font-size: 1.5em;
  margin: 5px;
  border-radius: 10px;
}
</style>
