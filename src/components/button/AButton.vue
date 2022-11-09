<template>
  <h1>父组件传入的数据：{{props.type}}</h1>
  <h1>子组件处理后的数据：{{theme}}</h1>
  <button class="a-button" :class="theme">
    <slot />
  </button>
</template>

<script setup>
import { computed } from "@vue/reactivity";

const props = defineProps({
  type: String,
});
const theme = computed(() => `a-button-${props.type}`);
console.log(theme);
</script>

<style lang="scss" scoped>
.a-button {
  padding: 0 20px;
  border-width: 1px;
  border-style: solid;
  border-color: #dcdfe6;
  border-radius: 4px;
  background-color: #fff;
  font-size: 14px;
  color: #606266;
  height: 40px;
}
.a-button-medium {
  height: 36px;
}
.a-button-small {
  padding: 0 15px;
  height: 32px;
  font-size: 12px;
}
.a-button-mini {
  padding: 0 15px;
  height: 28px;
  font-size: 12px;
}
.a-button[disabled] {
  opacity: 0.5;
  cursor: not-allowed;
}
.a-button-primary {
  background-color: #409eff;
  border-color: #409eff;
  color: #fff;
  &.is-border {
    background-color: transparent;
    color: #409eff;
  }
}
.a-button-success {
  background-color: #00d100;
  border-color: #00d100;
  color: #fff;
  &.is-border {
    background-color: transparent;
    color: #00d100;
  }
}
.a-button-warning {
  background-color: #e6a23c;
  border-color: #e6a23c;
  color: #fff;
  &.is-border {
    background-color: transparent;
    color: #e6a23c;
  }
}
.a-button-danger {
  background-color: #f56c6c;
  border-color: #f56c6c;
  color: #fff;
  &.is-border {
    background-color: transparent;
    color: #f56c6c;
  }
}
/**圆角 */
.is-round {
  border-radius: 100px;
}
</style>
