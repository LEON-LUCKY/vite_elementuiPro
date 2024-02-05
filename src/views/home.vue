<script setup>
import myMixTable from "../components/myMixTable.vue";

import { ref, onMounted } from "vue";
const dataList = ref([
  { title: "Act", list: [] },
  { title: "Aop", list: [] },
]);

const scrollBox = ref([
  [
    { year: 2021, icon: "🐂" },
    { year: 2022, icon: "🐯" },
  ],
  [
    { year: 2023, icon: "🐰" },
    { year: 2024, icon: "🐉" },
  ],
  [
    { year: 2025, icon: "🐍" },
    { year: 2025, icon: "🐎" },
  ],
]);
const displayYear = ref([]);
const index = ref(0);

for (let index = 0; index < 10; index++) {
  dataList.value[0].list.push({
    v: index * 10,
  });
  dataList.value[1].list.push({
    v: index * 10,
  });
}

const scroll = (type) => {
  if (index.value === 0 && type === "left") {
    return;
  }
  if (index.value === scrollBox.value.length - 1 && type === "right") {
    return;
  }
  if (type === "left") {
    index.value = index.value - 1;
  } else {
    index.value = index.value + 1;
  }
  displayYear.value = scrollBox.value[index.value];
  scrollBoxBgc.value = scrollBox.value[index.value][0].bgc;
};

onMounted(() => {
  displayYear.value = scrollBox.value[0];
});
</script>

<template>
  <h1>Home</h1>
  <div class="scroll_box">
    <div class="click_icon_lef" @click="scroll('left')">◀️</div>
    <ul class="scroll_container">
      <li
        class="scroll_item"
        :icon="item.icon"
        v-for="item in displayYear"
        :key="item"
      >
        {{ item.year }}
      </li>
    </ul>
    <div class="click_icon_right" @click="scroll('right')">▶️</div>
  </div>
  <myMixTable :data="dataList"></myMixTable>
</template>

<style scoped lang="less">
.scroll_box {
  margin: 100px auto;
  position: relative;
  width: 400px;
  height: 100px;
  border-radius: 50px;
  overflow: auto;
  // 隐藏滚动条
  -ms-overflow-style: none;
  scrollbar-width: none;
  &::-webkit-scrollbar {
    display: none;
  }
  background: linear-gradient(
    90deg,
    rgba(9, 60, 121, 0.6) 0%,
    rgba(0, 212, 255, 1) 100%
  );
  &:hover {
    .click_icon_lef,
    .click_icon_right {
      opacity: 0.8;
    }
  }
  .click_icon_lef,
  .click_icon_right {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    width: 50px;
    height: 50px;
    line-height: 50px;
    border-radius: 50px;
    background-color: rgba(0, 0, 0, 0.3);
    opacity: 0;
    transition: all 0.3s;
    user-select: none;
    cursor: pointer;
  }
  .click_icon_lef {
    left: 0;
  }
  .click_icon_right {
    right: 0;
  }
  .scroll_container {
    display: flex;
    align-items: center;
    // 去除默认的内外边距 和 列表样式
    padding: 0;
    margin: 0;
    list-style: none;
    // 子元素不压缩宽度
    white-space: nowrap;
    .scroll_item {
      flex: 1 0 200px;
      height: 100px;
      line-height: 100px;
      font-size: 24px;
      color: #fff;
      // 文字前面加圆形标记
      &::before {
        content: attr(icon);
        margin-right: 10px;
      }
    }
  }
}
</style>
