<script setup>
import myMixTable from "../components/myMixTable.vue"

import { ref } from 'vue'
const dataList = ref([
  { title: 'Act', list: [] },
  { title: 'Aop', list: [] },
])

for (let index = 0; index < 10; index++) {
  dataList.value[0].list.push({
    v: index * 10
  })
  dataList.value[1].list.push({
    v: index * 10
  })
}
</script>

<template>
  <h1>Home</h1>
  <myMixTable :data="dataList"></myMixTable>
</template>

<style scoped lang="less">

</style>