<script setup>
// import { ref } from 'vue'

const styleData = defineModel()

</script>

<template>
  <div class="boxPropertiesBox">
    <div class="boxPropertiesBox_title">Box Properties</div>
    <div class="boxPropertiesBox_form">
      <div class="boxPropertiesBox_form_item">
        <div class="boxPropertiesBox_form_item_title">
          Canvas color
        </div>
        <div class="boxPropertiesBox_form_item_input">
          <el-input v-model="styleData.canvasBgColor"></el-input>
        </div>
      </div>
      <div class="boxPropertiesBox_form_item">
        <div class="boxPropertiesBox_form_item_title">
          Background color
        </div>
        <div class="boxPropertiesBox_form_item_input">
          <el-input v-model="styleData.backgroundColor"></el-input>
        </div>
      </div>
      <div class="boxPropertiesBox_form_item">
        <div class="boxPropertiesBox_form_item_title">
          Border color
        </div>
        <div class="boxPropertiesBox_form_item_input">
          <el-input v-model="styleData.borderColor"></el-input>
        </div>
      </div>
      <div class="boxPropertiesBox_form_item">
        <div class="boxPropertiesBox_form_item_title">
          <span>Border radius</span>
          <div><el-input-number :max="20" :min="0" :controls="false" class="subInput"
              v-model="styleData.borderRadius" /><span>rem</span>
          </div>
        </div>
        <div class="boxPropertiesBox_form_item_input">
          <el-slider :min="0" :max="20" v-model="styleData.borderRadius" :show-tooltip="false" />
        </div>
      </div>
      <div class="boxPropertiesBox_form_item">
        <div class="boxPropertiesBox_form_item_title">
          <span>Height</span>
          <div><el-input-number :max="40" :min="0" :controls="false" class="subInput"
              v-model="styleData.height" /><span>rem</span></div>
        </div>
        <div class="boxPropertiesBox_form_item_input">
          <el-slider :min="0" :max="40" v-model="styleData.height" :show-tooltip="false" />
        </div>
      </div>
      <div class="boxPropertiesBox_form_item">
        <div class="boxPropertiesBox_form_item_title">
          <span>Width</span>
          <div><el-input-number :max="40" :min="0" :controls="false" class="subInput"
              v-model="styleData.width" /><span>rem</span>
          </div>
        </div>
        <div class="boxPropertiesBox_form_item_input">
          <el-slider :min="0" :max="40" v-model="styleData.width" :show-tooltip="false" />
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
:deep(.el-input__inner) {
  color: #333;
  height: 36px;
  font-size: 16px;
}

.boxPropertiesBox {
  width: 400px;
  height: calc(100vh - 64px - 64px);
  padding: 1rem;
  border-left: 1px solid #b9b9b9;

  .boxPropertiesBox_title {
    font-weight: 900;
  }

  .boxPropertiesBox_form {
    .boxPropertiesBox_form_item {
      margin-top: 30px;

      .boxPropertiesBox_form_item_title {
        font-weight: 800;
        display: flex;
        align-items: center;
        justify-content: space-between;

        .subInput {
          width: 50px;
          margin-right: 6px;
        }
      }

      .boxPropertiesBox_form_item_input {
        margin-top: 4px;
      }
    }
  }
}
</style>
