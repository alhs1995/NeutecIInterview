<script setup>
import sidebarItem from './sidebarItem.vue';
import { provide, onMounted, ref, inject, watch } from 'vue'
const props = defineProps({
  show: {
    type: Boolean,
    withDefaults: false
  }
})
const sideSelected = ref([])
// 將點選的選項存進去到localstorage就可以在關閉分頁之後又重新讀到數據了
// 不選用indexedDB或是Web SQL的原因是因為工期有點不太夠，不然性能和資料複雜度高一點的資料會比較好處理一點
onMounted(() => {
  if(localStorage.getItem('sideSelected')) {
    sideSelected.value = JSON.parse(localStorage.getItem('sideSelected'))
  }
})
watch(sideSelected,(newValue) => {
  localStorage.setItem('sideSelected', JSON.stringify(newValue))
})
provide('sidebarSelected', sideSelected)

const sideBarData = inject('StoreSidebar')
</script>

<template>
  <div class="sidebarContainer" :class="{'show': show}">
    <sidebarItem :level="1" :select-items-data="sideBarData" />
  </div>
</template>

<style lang="scss" scoped>
.sidebarContainer {
  width: 50%;
  height: 100%;
  position: absolute;
  right: -50%;
  top: 0;
  background-color: #000000ee;
  transition: right .3s linear;
  box-sizing: border-box;
  padding-top: 20px;
  &.show {
    right: 0;
  }
}
</style>