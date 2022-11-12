<template>
  <div class="home">
    <!-- <AButton type="success" :loading="flag" @parent-click="handlerClick"
      >默认按钮</AButton
    > -->
    <AButton type="success" :before-change="asyncFunction"
      >默认按钮</AButton
    >
    <AButton
      type="primary"
      block
      prefix="shangchuanshuju"
      vborder
      round
      size="small"
      >primary</AButton
    >
    <AButton
      type="success"
      suffix="icon-daohang"
      vborder
      round
      size="mini"
      disabled
      >success</AButton
    >
    <AButton type="warning" prefix="tongzhi" min-width="160px">warning</AButton>
    <AButton type="danger" suffix="xingxing" vborder min-width="300px"
      >danger</AButton
    >
  </div>
</template>

<script setup>
// @ is an alias to /src

import AButton from "../components/button/AButton.vue";

import { ref } from "vue";

const flag = ref(false);

const asyncFunction = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve();
    }, 3000);
  });
};

// 父组件通过 @parentClick 监听到子组件传递过来的parentClick事件后，触发handlerClick方法
// const handlerClick = (data) => {
//   console.log(data);
//   flag.value = true;
//   setTimeout(() => {
//     flag.value = false;
//     console.log("现在可以重新点击");
//   }, 3000);
// };
</script>

<style lang="scss" scoped></style>
