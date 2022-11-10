<template>
  <div class="home">
    <AButton size="small">默认按钮</AButton>
    <AButton type="primary" vborder>primary</AButton>
    <AButton type="success" vborder round>success</AButton>
    <AButton type="warning" round>warning</AButton>
    <AButton type="danger" size="mini" vborder disabled>danger</AButton>
  </div>
</template>

<script setup>
import AButton from "../components/button/AButton.vue";
</script>

<style lang="scss" scoped></style>
