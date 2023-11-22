<script setup>
import sidebarItem from './sidebarItem.vue';
import {  onMounted, inject } from 'vue'
const props = defineProps({
  show: {
    type: Boolean,
    withDefaults: false
  }
})

const sideSelected = inject('sidebarSelected')

onMounted(() => {
  if(localStorage.getItem('sideSelected')) {
    sideSelected.value = JSON.parse(localStorage.getItem('sideSelected'))
  }
})

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