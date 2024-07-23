<script setup>
const styleData = defineModel();
</script>

<template>
  <div class="customizeShadowsBox">
    <div class="customizeShadowsBox_title"><span>Customize Shadows</span><el-button type="primary">Add Shadow</el-button></div>

  </div>
</template>

<style scoped lang="scss">
.customizeShadowsBox {
  height: calc(100vh - 64px - 64px);
  overflow: auto;
  width: 400px;
  padding: 1rem;
  .customizeShadowsBox_title{
    font-weight: 900;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
}
</style>
