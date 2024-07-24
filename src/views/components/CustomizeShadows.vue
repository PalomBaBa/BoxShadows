<script setup>
import { ref } from 'vue';


const styleData = defineModel();

const activeNames = ref([]);

function addShadow() {
  styleData.value.shadows.push({
    key: Date.now(),
    active: true,
    inset: false,
    horizontalOffset: 10,
    verticalOffset: 0,
    blurRadius: 50,
    spreadRaduis: 0,
    color: 'rgba(0, 0, 0, 0.1)'
  })
}

function removeShadow(index) {
  styleData.value.shadows.splice(index, 1)
}
</script>

<template>
  <div class="customizeShadowsBox">
    <div class="customizeShadowsBox_title"><span>Customize Shadows</span><el-button type="primary"
        @click="addShadow">Add
        Shadow</el-button></div>
    <div class="customizeShadowsBox_shadowList">
      <el-collapse v-model="activeNames" v-if="styleData.shadows.length">
        <el-collapse-item :name="item.key" v-for="(item, index) in styleData.shadows" :key="item.key">
          <template #title>
            <span style="font-size: 18px;font-weight: 800;padding-left: 1rem;">{{ 'Shadow' + ' ' + (index + 1) }}</span>
          </template>
          <div class="customizeShadowsBox_shadowForm">
            <div class="customizeShadowsBox_shadowForm_topItem">
              <div>
                <el-checkbox v-model="item.active">Active</el-checkbox>
                <el-checkbox v-model="item.inset">Inset</el-checkbox>
              </div>
              <div><el-button type="danger" @click="removeShadow(index)">Remove</el-button></div>
            </div>
            <div class="customizeShadowsBox_shadowForm_item">
              <div class="customizeShadowsBox_shadowForm_item_title">
                <span>Horizontal offset</span>
                <div><el-input-number :max="100" :min="-100" :controls="false" class="subInput"
                    v-model="item.horizontalOffset" /><span>px</span>
                </div>
              </div>
              <div class="customizeShadowsBox_shadowForm_item_input">
                <el-slider :min="-100" :max="100" v-model="item.horizontalOffset" :show-tooltip="false" />
              </div>
            </div>
            <div class="customizeShadowsBox_shadowForm_item">
              <div class="customizeShadowsBox_shadowForm_item_title">
                <span>Vertical offset</span>
                <div><el-input-number :max="100" :min="-100" :controls="false" class="subInput"
                    v-model="item.verticalOffset" /><span>px</span>
                </div>
              </div>
              <div class="customizeShadowsBox_shadowForm_item_input">
                <el-slider :min="-100" :max="100" v-model="item.verticalOffset" :show-tooltip="false" />
              </div>
            </div>
            <div class="customizeShadowsBox_shadowForm_item">
              <div class="customizeShadowsBox_shadowForm_item_title">
                <span>Blur radius</span>
                <div><el-input-number :max="100" :min="0" :controls="false" class="subInput"
                    v-model="item.blurRadius" /><span>px</span>
                </div>
              </div>
              <div class="customizeShadowsBox_shadowForm_item_input">
                <el-slider :min="0" :max="100" v-model="item.blurRadius" :show-tooltip="false" />
              </div>
            </div>
            <div class="customizeShadowsBox_shadowForm_item">
              <div class="customizeShadowsBox_shadowForm_item_title">
                <span>Spread radius
                </span>
                <div><el-input-number :max="100" :min="-100" :controls="false" class="subInput"
                    v-model="item.spreadRaduis" /><span>px</span>
                </div>
              </div>
              <div class="customizeShadowsBox_shadowForm_item_input">
                <el-slider :min="-100" :max="100" v-model="item.spreadRaduis" :show-tooltip="false" />
              </div>
            </div>
            <div class="customizeShadowsBox_shadowForm_item">
              <div class="customizeShadowsBox_shadowForm_item_title">
                Color
              </div>
              <div class="customizeShadowsBox_shadowForm_item_input">
                <el-input v-model="item.color"></el-input>
              </div>
            </div>
          </div>
        </el-collapse-item>
      </el-collapse>
    </div>
  </div>
</template>

<style scoped lang="scss">
:deep(.el-collapse-item__content) {
  background: #f2f3f6;
  box-shadow: inset 0px 2px 5px -3px rgba(0, 0, 0, 0.1);
}

:deep(.is-active) {
  border-bottom: 1px solid #ebeef5;
}

.customizeShadowsBox {
  height: calc(100vh - 64px - 64px);
  overflow: auto;
  width: 400px;

  border-right: 1px solid #b9b9b9;

  .customizeShadowsBox_title {
    font-weight: 900;
    padding: 1rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .customizeShadowsBox_shadowList {
    margin-top: 14px;

    .customizeShadowsBox_shadowForm {

      padding: 18px 1rem 0;

      .customizeShadowsBox_shadowForm_topItem {
        display: flex;
        align-items: center;
        justify-content: space-between;
      }

      .customizeShadowsBox_shadowForm_item {
        margin-top: 18px;

        .customizeShadowsBox_shadowForm_item_title {
          font-weight: 800;
          font-size: 16px;
          display: flex;
          align-items: center;
          justify-content: space-between;

          .subInput {
            width: 60px;
            height: 36px;
            margin-right: 6px;
          }
        }

        .customizeShadowsBox_shadowForm_item_input {
          margin-top: 4px;
        }
      }
    }
  }
}
</style>
