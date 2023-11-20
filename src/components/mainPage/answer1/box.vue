<script setup>

</script>

<template>
  <div class="box"></div>
</template>

<style scoped>
.box {
  flex: 0 0 calc(calc(100% - 6px) / 3);
  height: 100px;
  border: black solid 2px;
  background: radial-gradient(circle, rgba(113,81,95,1) 81%, rgba(0,0,0,1) 100%);
  box-sizing: border-box;
}
</style>