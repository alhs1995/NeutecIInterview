<script setup>
import box from './box.vue'
</script>

<template>
  <div class="boxContainer">
    <box v-for="item in 9" :key="item" />
  </div>
</template>

<style scoped>
.boxContainer {
  width: 100%;
  height: 306px;
  display: flex;
  flex-wrap: wrap;
  align-content: space-between;
  justify-content: space-around;
}
</style>