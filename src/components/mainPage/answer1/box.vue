<script setup>
const props = defineProps({
  shine: {
    type: Boolean,
    withDefaults: false
  }
})
</script>

<template>
  <div class="box" :class="{'shine':props.shine}"></div>
</template>

<style lang="scss" scoped>
.box {
  flex: 0 0 calc(calc(100% - 6px) / 3);
  height: 100px;
  border: black solid 2px;
  background: radial-gradient(circle, rgba(113,81,95,1) 81%, rgba(0,0,0,1) 100%);
  box-sizing: border-box;
  &.shine{
    animation: shining 1s linear infinite;
  }
}
@keyframes shining {
  0%{
    opacity: 1;
  }
  50%{
    opacity: .6;
  }
  100%{
    opacity: 1;
  }
}
</style>