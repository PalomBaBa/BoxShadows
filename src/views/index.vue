<script setup>
import { ref } from 'vue';
import CustomizeShadows from './components/CustomizeShadows.vue';
import RenderArea from './components/RenderArea.vue';
import BoxProperties from './components/BoxProperties.vue';


const styleData = ref({
  canvasBgColor: '#f3f4f6',
  backgroundColor: '#fff',
  borderColor: 'transparent',
  borderRadius: 10,
  height: 20,
  width: 20,
  shadows: [
    {
      active: true,
      inset: false,
      horizontalOffset: 0,
      verticalOffset: 0,
      blurRadius: 50,
      spreadRaduis: 0,
      color: 'rgba(0, 0, 0, 0.1)'
    }
  ]
})

function showCssCode() {
  console.log(styleData.value);
}
</script>

<template>
  <div class="boxShadow_box">
    <div class="boxShadow_box_header">
      <div class="boxShadow_box_hearer_title">Box Shadows</div>
      <div class="boxShadow_box_hearer_showCodeBtn">
        <el-button type="primary" @click="showCssCode">Show code</el-button>
      </div>
    </div>

    <div class="boxShadow_box_content">
      <div class="boxShadow_box_content_left">
        <CustomizeShadows v-model="styleData" />
      </div>
      <div class="boxShadow_box_content_canvas">
        <RenderArea :styleData="styleData" />
      </div>
      <div class="boxShadow_box_content_right">
        <BoxProperties v-model="styleData" />
      </div>
    </div>

    <div class="boxShadow_box_footer">

    </div>
  </div>
</template>

<style scoped lang="scss">
.boxShadow_box {
  min-width: 1200px;
  height: 100vh;

  .boxShadow_box_header {
    height: 64px;
    border-bottom: 1px solid #b9b9b9;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 30px;

    .boxShadow_box_hearer_title {
      font-size: 20px;
      font-weight: bolder;
    }

    .boxShadow_box_hearer_showCodeBtn {
      .el-button--primary {
        font-size: 16px;
      }
    }
  }

  .boxShadow_box_content {
    display: flex;
    height: calc(100vh - 64px - 64px);
    display: flex;
    justify-content: space-between
  }

  .boxShadow_box_footer {
    height: 64px;
    border-top: 1px solid #b9b9b9;
  }
}
</style>
