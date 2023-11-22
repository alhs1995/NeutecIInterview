<script setup>
import box from './box.vue'
import dot from './dot.vue'
import { ref } from 'vue'
// 指定箱子要不要閃爍
const boxSetting = ref([
  false,
  false,
  true,
  false,
  true,
  false,
  false,
  false,
  true
])
// 寫個算單位的方便處理位置
const getSet = (times) => {
  const setTimes = (2*times)+1
  const setAdd = 3*times
  if(setTimes===1) {
    return `calc(calc(100% - 6px) / 6)`
  } else {
    return `calc(calc(calc(calc(100% - 6px) / 6) * ${setTimes}) + ${setAdd}px)`
  }
}
// 點點要多少個都可以，可以直接指定結束位置(額外需求2、3)
const dots = ref([
  {
    StartX: getSet(0),
    StartY: getSet(0),
    EndX: getSet(2),
    EndY: getSet(0),
  },
  {
    StartX: getSet(2),
    StartY: getSet(0),
    EndX: getSet(4),
    EndY: getSet(0),
  },
  {
    StartX: getSet(0),
    StartY: getSet(2),
    EndX: getSet(2),
    EndY: getSet(2),
  },
  {
    StartX: getSet(2),
    StartY: getSet(2),
    EndX: getSet(4),
    EndY: getSet(2),
  },
])
</script>

<template>
  <div class="boxContainer">
    <box v-for="(box,index) in boxSetting" :key="'box'+index" :shine="box" />
    <dot 
      v-for="(dot,index) in dots" 
      :key="'dot'+index" 
      :start-x="dot.StartX" 
      :start-y="dot.StartY"
      :end-x="dot.EndX"
      :end-y="dot.EndY"
    />
  </div>
</template>

<style lang="scss" scoped>
.boxContainer {
  width: 100%;
  height: 306px;
  display: flex;
  flex-wrap: wrap;
  align-content: space-between;
  justify-content: space-around;
  position: relative;
  overflow: hidden;
}

</style>