<template>
  <button
    class="a-button"
    :class="[vtype, isBorder, isRound, vsize, blockCss]"
    :disabled="disabled"
    :style="[minWidthCss]"
  >
    <span>
      <i v-if="iconPrefix" class="iconfont icon-prefix" :class="iconPrefix"></i>
      <slot />
      <i v-if="iconSuffix" class="iconfont icon-suffix" :class="iconSuffix"></i>
    </span>
  </button>
</template>

<script setup>
import { computed } from "@vue/reactivity";

const props = defineProps({
  type: {
    type: String,
    default: "",
  },
  size: {
    size: String,
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
  vborder: Boolean,
  round: Boolean,
  disabled: Boolean,
  block: Boolean,
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
  return props.block ? 'a-button-block' : "";
});
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
  + .a-button {
    margin-left: 14px;
  }
  > span {
    display: flex;
    align-items: center;
    justify-content: center;
  }
  i {
    width: 14px;
    height: 14px;
  }
  .icon-prefix {
    margin-right: 10px;
  }
  .icon-suffix {
    margin-left: 10px;
  }
}
.a-button-medium {
  height: 36px;
}
.a-button-small {
  padding: 0 15px;
  height: 32px;
  font-size: 12px;
  .icon-prefix {
    margin-right: 5px;
  }
  .icon-suffix {
    margin-left: 5px;
  }
}
.a-button-mini {
  padding: 0 15px;
  height: 28px;
  font-size: 12px;
  .icon-prefix {
    margin-right: 5px;
  }
  .icon-suffix {
    margin-left: 5px;
  }
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
/**块级按钮 */
.a-button-block {
  display: block;
  width: 100%;
}
</style>
