<template>
  <div class="time-capsule">
    <div class="title">
      <hourglass-full
        theme="two-tone"
        size="24"
        :fill="['#efefef', '#00000020']"
      />
      <span>時光膠囊</span>
    </div>
    <span class="text"
      >今日已經度過了&nbsp;{{ timeData.day.start }}&nbsp;小时</span
    >
    <el-progress
      :text-inside="true"
      :stroke-width="20"
      :percentage="timeData.day.pass"
    />
    <span class="text"
      >本週已經度過了&nbsp;{{ timeData.week.start }}&nbsp;天</span
    >
    <el-progress
      :text-inside="true"
      :stroke-width="20"
      :percentage="timeData.week.pass"
    />
    <span class="text"
      >本月已經度過了&nbsp;{{ timeData.month.start }}&nbsp;天</span
    >
    <el-progress
      :text-inside="true"
      :stroke-width="20"
      :percentage="timeData.month.pass"
    />
    <span class="text"
      >今年已經度過了&nbsp;{{ timeData.year.start }}&nbsp;个月</span
    >
    <el-progress
      :text-inside="true"
      :stroke-width="20"
      :percentage="timeData.year.pass"
    />
    <div v-if="startDateText && store.siteStartShow">
      <span class="text" v-html="startDateText" />
      <!-- <el-progress
        :show-text="false"
        :indeterminate="true"
        :stroke-width="6"
        :percentage="80"
        :duration="2"
      /> -->
    </div>
  </div>
</template>

<script setup>
import { onMounted, onBeforeUnmount, ref } from "vue";
import { HourglassFull } from "@icon-park/vue-next";
import { getTimeCapsule, siteDateStatistics } from "@/utils/getTime.js";
import { mainStore } from "@/store";
const store = mainStore();

// 进度条数据
let timeData = ref(getTimeCapsule());
let startDate = ref(import.meta.env.VITE_SITE_START);
let startDateText = ref(null);
let timeInterval = null;

onMounted(() => {
  timeInterval = setInterval(() => {
    timeData.value = getTimeCapsule();
    if (startDate.value)
      startDateText.value = siteDateStatistics(new Date(startDate.value));
  }, 1000);
});

onBeforeUnmount(() => {
  clearInterval(timeInterval);
});
</script>

<style lang="scss" scoped>
.time-capsule {
  width: 100%;
  .title {
    display: flex;
    flex-direction: row;
    align-items: center;
    margin: 0.2rem 0 1.5rem;
    font-size: 1.1rem;
    .i-icon {
      display: flex;
      justify-content: center;
      align-items: center;
      margin-right: 6px;
    }
  }
  .text {
    display: block;
    margin: 1rem 0rem 0.5rem 0rem;
    font-size: 0.95rem;
  }
}
</style>
