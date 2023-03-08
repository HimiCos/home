<template>
  <div class="setting">
    <el-collapse class="collapse" v-model="activeName" accordion>
      <el-collapse-item title="壁紙設置" name="1">
        <div class="bg-set">
          <el-radio-group v-model="bgSet" text-color="#ffffff">
            <el-radio label="0" size="large" border>默認壁紙</el-radio>
            <el-radio label="1" size="large" border>每日一圖</el-radio>
            <el-radio label="2" size="large" border>隨機風景</el-radio>
            <el-radio label="3" size="large" border>隨機動漫</el-radio>
          </el-radio-group>
        </div>
      </el-collapse-item>
      <el-collapse-item title="其他設置" name="2">
        <div class="item">
          <span class="text">建站日期顯示</span>
          <el-switch
            v-model="siteStartShow"
            inline-prompt
            :active-icon="CheckSmall"
            :inactive-icon="CloseSmall"
          />
        </div>
      </el-collapse-item>
      <el-collapse-item title="其他設置" name="3">
        <div>設置內容待增加</div>
      </el-collapse-item>
      <el-collapse-item title="其他設置" name="4">
        <div>設置內容待增加</div>
      </el-collapse-item>
    </el-collapse>
  </div>
</template>

<script setup>
import { ref, onMounted, watch } from "vue";
import { mainStore } from "@/store";
import { CheckSmall, CloseSmall } from "@icon-park/vue-next";
import { storeToRefs } from "pinia";

const store = mainStore();
const { siteStartShow } = storeToRefs(store);

// 默认选中项
let activeName = ref("1");
let bgSet = ref("0");

onMounted(() => {
  bgSet.value = store.coverType.toString();
});

// 壁纸选中项
watch(
  () => bgSet.value,
  (value) => {
    store.coverType = value;
  }
);
</script>

<style lang="scss" scoped>
.setting {
  .collapse {
    border-radius: 8px;
    --el-collapse-content-bg-color: #ffffff10;
    border-color: transparent;
    overflow: hidden;

    :deep(.el-collapse-item__header) {
      background-color: #ffffff30;
      color: #fff;
      font-size: 15px;
      padding-left: 18px;
      border-color: transparent;
    }

    :deep(.el-collapse-item__wrap) {
      border-color: transparent;

      .el-collapse-item__content {
        padding: 20px;
        .item {
          display: flex;
          align-items: center;
          justify-content: space-between;
          font-size: 14px;
          .el-switch__core {
            border-color: transparent;
            background-color: #ffffff30;
          }
        }
        .bg-set {
          .el-radio-group {
            justify-content: space-between;

            .el-radio {
              margin: 10px 16px;
              background: #ffffff26;
              border: 2px solid transparent;
              border-radius: 8px;

              .el-radio__label {
                color: #fff;
              }

              .el-radio__inner {
                background: #ffffff06 !important;
                border: 2px solid #eeeeee !important;
              }

              &.is-checked {
                background: #ffffff06 !important;
                border: 2px solid #eeeeee !important;
              }

              .is-checked {
                .el-radio__inner {
                  background-color: #ffffff30 !important;
                  border-color: #fff !important;
                }

                & + .el-radio__label {
                  color: #fff !important;
                }
              }
            }
          }
        }
      }
    }
  }
}
</style>
