<script setup>
import { ref, watch, onMounted } from 'vue';
import CustomizeShadows from './components/CustomizeShadows.vue';
import RenderArea from './components/RenderArea.vue';
import BoxProperties from './components/BoxProperties.vue';
import CopyDialog from './components/CopyDialog.vue';


const copyDialogRef = ref(null);

const styleData = ref({
  canvasBgColor: '#f3f4f6',
  backgroundColor: '#fff',
  borderColor: 'transparent',
  borderRadius: 10,
  height: 20,
  width: 20,
  boxShadow: '',
  shadows: [
    {
      key: Date.now(),
      active: true,
      inset: false,
      horizontalOffset: 10,
      verticalOffset: 0,
      blurRadius: 50,
      spreadRaduis: 0,
      color: 'rgba(0, 0, 0, 0.1)'
    }
  ]
})

function showCssCode() {
  console.log(styleData.value);
  copyDialogRef.value.open()

}

function handleBoxShadow() {
  let data = '';
  if (styleData.value.shadows.length && styleData.value.shadows.length > 1) {
    styleData.value.shadows.forEach((item, index) => {
      if (item.active) {
        if (item.inset) {
          if (index + 1 === styleData.value.shadows.length) {
            data += `inset ${item.horizontalOffset}px ${item.verticalOffset}px ${item.blurRadius}px ${item.spreadRaduis}px ${item.color}`
          } else {
            data += `inset ${item.horizontalOffset}px ${item.verticalOffset}px ${item.blurRadius}px ${item.spreadRaduis}px ${item.color},`
          }
        } else {
          if (index + 1 === styleData.value.shadows.length) {
            data += `${item.horizontalOffset}px ${item.verticalOffset}px ${item.blurRadius}px ${item.spreadRaduis}px ${item.color}`
          } else {
            data += `${item.horizontalOffset}px ${item.verticalOffset}px ${item.blurRadius}px ${item.spreadRaduis}px ${item.color},`
          }
        }
      }
    })
  } else {
    styleData.value.shadows.forEach((item, index) => {
      if (item.active) {
        if (item.inset) {
          data += `inset ${item.horizontalOffset}px ${item.verticalOffset}px ${item.blurRadius}px ${item.spreadRaduis}px ${item.color}`
        } else {
          data += `${item.horizontalOffset}px ${item.verticalOffset}px ${item.blurRadius}px ${item.spreadRaduis}px ${item.color}`
        }
      }
    })
  }
  console.log('data: ', data);
  styleData.value.boxShadow = data
}

watch(() => styleData.value.shadows, () => {
  handleBoxShadow()
}, {
  deep: true
})

onMounted(() => {
  handleBoxShadow()
})
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


    <CopyDialog v-model="styleData" ref="copyDialogRef" />
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
