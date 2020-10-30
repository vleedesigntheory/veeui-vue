<template>
  <button class="vee-button" :class="btnClass" :disabled="loading" @click="$emit('click',$event)">
      <vee-icon :icon="icon" v-if="icon && !loading" class="icon"></vee-icon>
      <vee-icon icon="loading" v-if="loading" class="icon"></vee-icon>
      <span v-if="this.$slots.default">
        <slot></slot>
      </span>
  </button>
</template>

<script lang="ts">
import { computed, defineComponent } from 'vue';

export default defineComponent({
  name: 'vee-button',
  props: {
    type: {
        type: String,
        default: ''
    },
    icon: {
        type: String
    },
    iconPosition: {
        type: String,
        default: 'left'
    },
    loading: {
        type: Boolean,
        default: false
    }
  },
  components: {
    
  },
  setup(props) {
    const btnClass = computed(() => {
        let classes = [];
        if(props.type) {
            classes.push(`vee-button-${props.type}`)
        }
        if(props.iconPosition) {
            classes.push(`vee-button-${props.iconPosition}`)
        }
        return classes;
    })

    return {
        btnClass
    }
  }
});
</script>

<style lang="scss">
@import '@/styles/_var.scss';
$height: 42px;
$font-size: 16px;
$color: #606266;
$border-color: #dcdfe6;
$background: #ecf5ff;
$active-color: #3a8ee6;
.vee-button {
    border-radius: $border-radius;
    border: 1px solid $border-color;
    height: $height;
    font-size: $font-size;
    cursor: pointer;
    line-height: 1;
    padding: 12px 20px;
    display: inline-flex;
    justify-content: center;
    vertical-align: middle;
    user-select: none;
    &:hover {
        border-color: $border-color;
        background-color: $background;
    }
    &:focus, &:active {
        color: $active-color;
        border: 1px solid $active-color;
        background-color: $background;
        outline: none;
    }
    @each $type, $color in (primary: $primary, success: $success, info: $info, warning: $warning, danger: $danger) {
        &-#{$type} {
            background: #{$color};
            border: 1px solid #{$color};
            color: #fff;
            fill: #fff;
        }
    }
    @each $type, $color in (primary: $primary-hover, success: $success-hover, info: $info-hover, warning: $warning-hover, danger: $danger-hover) {
        &-#{$type}:hover {
            background: #{$color};
            border: 1px solid #{$color};
            color: #fff;
        }
    }
    @each $type, $color in (primary: $primary-active, success: $success-active, info: $info-active, warning: $warning-active, danger: $danger-active) {
        &-#{$type}:active, &-#{$type}:focus {
            background: #{$color};
            border: 1px solid #{$color};
            color: #fff;
        }
    }
    .icon {
        width: 16px;
        height: 16px;
    }
    .icon + span {
        margin-left: 4px;
    }
    &-left {
        svg {order:1}
        span {order:2}
    }
    &-right {
        span {order:1}
        svg {order:2}
        .icon + span {
            margin-left: 0;
            margin-right: 4px;
        }
    }
    &[disabled] {
        cursor: not-allowed;
    }
}
</style>