<script setup>
import { ref } from 'vue';
import { ElNotification } from 'element-plus'


const styleData = defineModel();
console.log('styleData: ', styleData.value);

const dialogVisible = ref(false);

function open() {
  dialogVisible.value = true;
}

function close() {
  dialogVisible.value = false;
}

async function copyCss() {
  let copyData = 'box-shadow:' + styleData.value.boxShadow;
  try {
    await navigator.clipboard.writeText(copyData);
    ElNotification({
      title: 'Success',
      message: 'Copy success',
      type: 'success',
    })
  } catch (err) {
    ElNotification({
      title: 'Error',
      message: 'Copy failed',
      type: 'error',
    })
  }
}

defineExpose({
  open
})
</script>

<template>
  <div>
    <el-dialog align-center v-model="dialogVisible" width="600">
      <div class="copyDialogBox">
        <div class="copyDialogBox_title">Generated Styles</div>
        <div class="copyDialogBox_subTitle">This is the CSS needed to generate the box shadows you see in the app.</div>
        <div class="copyDialogBox_content">
          <div v-if="styleData.shadows.length === 0">Please apply at least one active shadow</div>
          <div class="copyDialogBox_content_exist" v-else>
            <div class="copyDialogBox_content_data">
              <span style="color: #2563eb;">box-shadow:</span> {{ styleData.boxShadow }}
            </div>
            <div class="copyDialogBox_content_data_copy" @click="copyCss"><el-icon>
                <DocumentCopy />
              </el-icon>Copy</div>
          </div>
        </div>
        <div class="copyDialogBox_closeBtn">
          <el-button type="primary" @click="close">Close</el-button>
        </div>
      </div>
    </el-dialog>
  </div>
</template>

<style scoped lang=scss>
.copyDialogBox {
  color: #333;

  .copyDialogBox_title {
    font-size: 28px;
    font-weight: 800;
  }

  .copyDialogBox_subTitle {
    font-size: 16px;
    margin-top: 10px;
  }

  .copyDialogBox_content {
    margin-top: 10px;
    font-size: 16px;

    .copyDialogBox_content_exist {
      display: flex;
      align-items: center;

      .copyDialogBox_content_data {
        width: 480px;
        display: flex;
        align-items: center;
        padding: 0 20px;
        overflow: auto;
        border-radius: 4px;
        border: 1px solid #e6e6e6;
        height: 50px;
        font-size: 14px;
        font-weight: 800;
        text-wrap: nowrap;
        background: #f8f8f8;
      }

      .copyDialogBox_content_data_copy {
        width: 80px;
        font-weight: 800;
        margin-left: 10px;
        cursor: pointer;
        display: flex;
        align-items: center;
        justify-content: center;
        border-radius: 4px;
        border: 1px solid #e6e6e6;
        height: 50px;
        font-size: 14px;
        background: #f8f8f8;
      }
    }
  }

  .copyDialogBox_closeBtn {
    display: flex;
    margin-top: 20px;
    justify-content: flex-end;
  }
}
</style>
