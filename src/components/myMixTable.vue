<script setup>
import { computed } from "vue";
defineProps({
  data: {
    type: Array,
    default() {
      return [];
    },
  },
});
const clickHandler = (v) => {
  console.log(v);
};
</script>

<template>
  <div class="mixTable_box">
    <div class="header_utils"></div>
    <div class="body_content">
      <div class="content_item" v-for="item in data" :key="item">
        <div class="content_item_header">
          <div class="header_title">{{ item.title }}</div>
          <div class="sort_icon_box">
            <el-icon class="sort_item"><CaretTop /></el-icon>
            <el-icon class="sort_item"><CaretBottom /></el-icon>
          </div>
        </div>
        <div class="content_item_body">
          <template v-for="(d, i) in item.list" :key="i">
            <div class="data_box">
              <span class="data_item">{{ d.v }}</span>
            </div>
          </template>
        </div>
      </div>
    </div>
    <!-- 点击区域 -->
    <div class="click_row_bar_box">
      <div class="click_row_bar_h"></div>
      <div class="click_row_bar_b">
        <div
          class="click_row_bar"
          v-for="(item, index) in 10"
          :key="index"
          @click="clickHandler(index)"
        ></div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="less">
@header-h: 50px;
.mixTable_box {
  width: 400px;
  height: 500px;
  display: flex;
  flex-direction: column;
  background: hotpink;
  border: 1px solid #000;
  box-sizing: border-box;
  position: relative;
  .header_utils {
    display: flex;
  }
  .body_content {
    display: flex;
    height: 100%;
    background: red;
    position: relative;
    box-sizing: border-box;
    .content_item {
      flex: 1 1 100px;
      display: flex;
      flex-direction: column;
      border: 1px solid #ccc;
      box-sizing: border-box;
      .content_item_header {
        flex: 0 1 @header-h;
        background-color: pink;
        display: flex;
        align-items: center;
        .header_title {
          flex: 1 0;
        }
        .sort_icon_box {
          flex: 0 1 30px;
          display: flex;
          flex-direction: column;
          .sort_item {
            cursor: pointer;
            &:hover {
              color: green;
            }
          }
        }
      }
      .content_item_body {
        flex: 1 1 50px;
        background-color: #fff;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        .data_box {
          flex: 1;
          width: calc(100% - 50px);
          text-align: center;
          .data_item {
            margin: auto 0;
            height: 100%;
          }
        }
      }
    }
  }
  .click_row_bar_box {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    display: flex;
    flex-direction: column;
    background-color: rgba(0, 0, 0, 0);
    z-index: 9;
    .click_row_bar_h {
      flex: 0 1 @header-h;
    }
    .click_row_bar_b {
      flex: 1 1 50px;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      .click_row_bar {
        flex: 1;
        &:hover {
          background-color: rgba(215, 96, 94, 0.5);
        }
      }
    }
  }
}
</style>
