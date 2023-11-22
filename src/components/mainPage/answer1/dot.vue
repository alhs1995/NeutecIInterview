<script setup>
const props = defineProps({
  startX: {
    type: String
  },
  startY: {
    type: String
  },
  endX: {
    type: String
  },
  endY: {
    type: String
  },
})
</script>

<template>
  <div class="dot" :style="{'--startX':props.startX, '--startY':props.startY, '--endX':props.endX, '--endY':props.endY}">0</div>
</template>

<style lang="scss" scoped>
// animation動畫(動畫種類1)
.dot {
  width: 30px;
  height: 30px;
  background-color: #A5F12B;
  border-radius: 50%;
  position: absolute;
  transform: translate(-50%, -50%);
  top: var(--startY);
  left: var(--startX);
  display: flex;
  align-items: center;
  justify-content: center;
  animation: flyTo 1s ease infinite;
  @keyframes flyTo {
    to{
      top: var(--endY);
      left: var(--endX);
    }
  }
}
</style>