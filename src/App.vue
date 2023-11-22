<script setup>
import { provide, ref, onMounted, shallowRef } from 'vue'
import data from './assets/data.json'

// 設定接進來的參數
const StoreSidebar = ref([])
provide("StoreSidebar", StoreSidebar)
// 假的API
const fakeApi = () => {
  return new Promise((reslove, reject) => {
    reslove(data)
  })
}

onMounted(() => {
  // 模擬API呼叫
  fakeApi().then(
    res => {
      StoreSidebar.value = res
    }
  )
})
  
// sidebar開關控制
const show = ref(false)
const onSideOpenClick = () => {
  show.value = true
}
const onSlideCloseClick = () => {
  show.value = false
}
provide("sidebarShow", show)

import sideBar from "./components/sidebar/sidebar.vue"
const selectedSideComponent = shallowRef(sideBar)

import mainAnswer1 from "./components/mainPage/answer1/index.vue"
const selectedMainComponent = shallowRef(mainAnswer1)


</script>

<template>
  <div class="mainBg" @click="onSlideCloseClick">
    <div class="top">
      <!-- <select>
        <option value=""></option>
      </select> -->
      <button @click.stop="onSideOpenClick">
        <img src="./assets/menu.svg">
      </button>
    </div>
    <component :is="selectedMainComponent" />
    <component :is="selectedSideComponent" :show="show" @click.stop />
  </div>
</template>  

<style lang="scss" scoped>
.mainBg {
  background-color: #a3a3a3;
  height: 100vh;
  width: 100vw;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  position: relative;
  overflow-x: hidden;
}
.top {
  height: 32px;
  width: 100%;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  box-sizing: border-box;
  padding-right: 7px;
  background-color: #fff;
  button {
    display: flex;
    align-items: center;
    img {
      width: 17px;
    }
  }
}

</style>
