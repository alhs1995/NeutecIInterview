<script setup>
import sidebarItem from './sidebarItem.vue'
import { inject, computed } from 'vue'
const props = defineProps({
  level: {
    type: Number,
    required: true
  },
  selectItemsData: {
    type: Array,
  }
})
const sidebarSelected = inject('sidebarSelected')
const thisSelected = computed(() => {
  return props.selectItemsData.find(element=>element.key==sidebarSelected.value[props.level-1]) ?? {key:''}
})
const onSelectClick = (key) => {
  let tmpSelectArray = sidebarSelected.value
  tmpSelectArray[props.level-1] = key
  sidebarSelected.value = tmpSelectArray.slice(0,props.level)
}
</script>

<template>
  <div class="itemList">
    <div 
      v-for="(item,index) in props.selectItemsData" 
      :key="'selectItem'+level+index" 
      class="sidebarItem"
      :class="{'show': item.key==thisSelected.key}"
      @click.stop="onSelectClick(item.key)"
    >
      <div class="itemShow">
        {{ item.text }}
      </div>
      <sidebarItem 
        v-if="item.key==thisSelected.key && thisSelected.children && thisSelected.children.length > 0 && thisSelected.children != {}" 
        :level="props.level+1"
        :select-items-data="thisSelected.children"
      />
    </div>
  </div>
</template>

<style lang="scss" scoped>
.itemList {
  display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  cursor: pointer;
  .sidebarItem {
    color: #fff;
    padding-left: 10px;
    font-size: 16px;
    flex: 0 0 32px;
    display: flex;
    flex-direction: column;
    flex-wrap: nowrap;
    justify-content: center;
    &.show {
      color: rgb(255, 255, 0);
      background-color: #b8b8b8;
    }
    .itemShow {
      flex: 0 0 32px;
      display: flex;
      align-items: center;
    }
  }
}
</style>