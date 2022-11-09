<template>
  <div class="home">
    <AButton :type="type">{{type}}</AButton>
  </div>
</template>

<script setup>
import AButton from "../components/button/AButton.vue";

const type = "success";
</script>

<style lang="scss" scoped></style>
