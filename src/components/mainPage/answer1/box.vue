<script setup>
import { onBeforeUnmount, onMounted, ref } from "vue"

const props = defineProps({
  shine: {
    type: Boolean,
    withDefaults: false
  }
})
let shining = ref(false)
let startShineLoop;
onMounted(() => {
  if(props.shine) {
    startShineLoop = setInterval(()=>{
      shining.value = !shining.value
    },1000)
  }
})
onBeforeUnmount(() => {
  if(startShineLoop) clearInterval(startShineLoop)
})
</script>

<template>
  <div class="box" :class="{'shine':shining}"></div>
</template>

<style lang="scss" scoped>
// transition(動畫種類2)
.box {
  flex: 0 0 calc(calc(100% - 6px) / 3);
  height: 100px;
  border: black solid 2px;
  background: radial-gradient(circle, rgba(113,81,95,1) 81%, rgba(0,0,0,1) 100%);
  box-sizing: border-box;
  opacity: 1;
  transition: opacity 1s linear;
  &.shine {
    opacity: .6;
  }
}
</style>