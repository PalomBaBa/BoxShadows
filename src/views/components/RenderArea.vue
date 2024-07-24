<script setup>
import { ref, watch } from 'vue';


const props = defineProps({
  styleData: {
    type: Object,
    default: () => { }
  }
})

const styleData = ref(props.styleData);
console.log('styleData: ', styleData.value);

watch(() => props.styleData, val => {
  console.log('val: ', val);
  styleData.value = val;
})

function handleBoxShadow() {
  console.log(styleData.value)
}
</script>

<template>
  <div class="renderAreaBox" v-if="styleData" :style="{ backgroundColor: styleData.canvasBgColor }">
    <div class="renderItem" :style="{
    backgroundColor: styleData.backgroundColor,
    border: `1px solid ${styleData.borderColor}`,
    width: `${styleData.width}rem`,
    height: `${styleData.height}rem`,
  borderRadius: `${styleData.borderRadius}rem`,
    boxShadow:`${styleData.boxShadow}`
  }"></div>
  </div>
</template>

<style>
.renderAreaBox {
  min-width: 800px;
  width: calc(100vw - 400px - 400px);
  height: calc(100vh - 64px - 64px);
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
