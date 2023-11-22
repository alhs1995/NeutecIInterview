<script setup>
import { inject, computed, ref, watch } from 'vue'
const StoreSidebar = inject('StoreSidebar')
const sidebarSelected = inject('sidebarSelected')
const flatItem = (arr,level) => {
  return arr.map(ele => {
    let rtnArr = [{key: ele.key, text: ele.text,level:level}]
    if(Object.prototype.hasOwnProperty.call(ele,'children')){
      rtnArr.push(flatItem(ele.children,level+1))
    }
    return rtnArr
  })
}
const selectItems = computed(()=>flatItem(StoreSidebar.value,0).flat(Infinity))

const selectedItem = ref('')
const selectedItemList = ref([])
const findData = (findArray) => {
  return findArray.find(e=>{
    if(e.key==selectedItem.value) {
      selectedItemList.value.unshift(e.key)
      return true
    } else {
      if(Object.prototype.hasOwnProperty.call(e,'children')){
        const rtnBool = findData(e.children)
        if(rtnBool) selectedItemList.value.unshift(e.key)
        return rtnBool
      } else {
        return false
      }
    }
  })
}
watch(selectedItem, async function() {
  selectedItemList.value = []
  await findData(StoreSidebar.value)
  sidebarSelected.value = selectedItemList.value
})
</script>

<template>
  <select v-model="selectedItem">
    <option v-for="(item,index) in selectItems" :key="'selectItem'+index" :value="item.key">{{ item.text }}</option>
  </select>
</template>

<style lang="scss" scoped>

</style>