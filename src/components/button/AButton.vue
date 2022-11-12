<template>
  <button
    @click="change"
    class="a-button"
    :class="[vtype, isBorder, isRound, vsize, blockCss]"
    :disabled="disabled || loading || load"
    :style="[minWidthCss]"
  >
    <span>
      <i v-if="loading || load" class="iconfont icon-prefix icon-loading"></i>
      <i v-if="iconPrefix" class="iconfont icon-prefix" :class="iconPrefix"></i>
      <slot />
      <i v-if="iconSuffix" class="iconfont icon-suffix" :class="iconSuffix"></i>
    </span>
  </button>
</template>

<script setup>
import { computed } from "@vue/reactivity";
import { ref } from "vue";
const props = defineProps({
  type: {
    type: String,
    default: "",
  },
  size: {
    type: String,
    default: "",
  },
  minWidth: {
    type: String,
    default: "",
  },
  prefix: {
    type: String,
    default: "",
  },
  suffix: {
    type: String,
    default: "",
  },
  loading: Boolean,
  vborder: Boolean,
  round: Boolean,
  disabled: Boolean,
  block: Boolean,
  beforeChange: Function,
});
const vtype = computed(() => {
  return props.type ? `a-button-${props.type}` : "";
});
const vsize = computed(() => {
  return props.size ? `a-button-${props.size}` : "";
});
const isBorder = computed(() => {
  return props.vborder ? "is-border" : "";
});
const isRound = computed(() => {
  return props.round ? "is-round" : "";
});
const minWidthCss = computed(() => {
  if (!props.minWidth) {
    return "";
  }
  return { "min-width": props.minWidth };
});
// 前缀图标处理
const iconPrefix = computed(() => {
  return props.prefix ? `icon-${props.prefix}` : "";
});
// 后缀图标处理
const iconSuffix = computed(() => {
  return props.suffix ? `icon-${props.suffix}` : "";
});
// 设置块级元素
const blockCss = computed(() => {
  return props.block ? "a-button-block" : "";
});

// 定义一个子传父事件-parentClick
const emits = defineEmits(["parentClick"]);
// 点击按钮时候通过change方法将parentClick 发射给父组件
// const change = () => emits("parentClick",'我是子组件传递的信息');
const load = ref(false);
const change = () => {
  if (typeof props.beforeChange === "function") {
    load.value = true;
    props
      .beforeChange()
      .then((response) => {
        load.value = false;
      })
      .catch(() => {
        load.value = false;
      });
  }
  emits("parentClick", "我是子组件传递的信息");
};
</script>

<style lang="scss" scoped>
@import './button.scss'
</style>
