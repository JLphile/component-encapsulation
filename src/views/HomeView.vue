<template>
  <div class="home">
<<<<<<< HEAD
    <AButton>默认按钮</AButton>
    <AButton type="primary" vborder>primary</AButton>
    <AButton type="success" vborder round>success</AButton>
    <AButton type="warning" round>warning</AButton>
    <AButton type="danger" size="mini" vborder disabled>danger</AButton>
=======
    <AButton :type="type">{{type}}</AButton>
>>>>>>> 4494f7ebb79a7aa53a77fcc518de3ff4a4618d9b
  </div>
</template>

<script setup>
import AButton from "../components/button/AButton.vue";
<<<<<<< HEAD
=======

const type = "success";
>>>>>>> 4494f7ebb79a7aa53a77fcc518de3ff4a4618d9b
</script>

<style lang="scss" scoped></style>
