<template>
  <button
    :data-id="id"
    :disabled="disabled || loading"
    v-bind="$attrs"
    :class="[
      'base-button',
      type,
      size,
      { selected: selected },
      { shadow: shadow, disabled: disabled },
    ]"
    :type="buttonType || 'button'"
    v-on="listeners"
    @click="routeTo()"
  >
    <div class="base-button-text" :class="[{ center }]">
      <BaseIcon
        v-if="showIcon && !iconRight"
        clickable
        style="padding-right: 2px"
        :shared-id="id"
        :icon="icon"
        :color="iconColor"
        :size="iconSize ? iconSize : size"
      />
      <BaseIcon
        v-if="loading"
        clickable
        style="padding-right: 2px"
        :shared-id="id"
        icon="loading"
        :color="iconColor"
        spin
        :size="iconSize ? iconSize : size"
      />
      <slot>
        {{ label }}
      </slot>
    </div>
    <div
      v-if="showIcon && iconRight && !loading && label"
      style="padding-right: 5px"
    />
    <BaseIcon
      v-if="showIcon && iconRight"
      clickable
      :shared-id="id"
      :icon="icon"
      :color="iconColor"
      :size="size"
    />
  </button>
</template>

<script>
export default {
  inheritAttrs: false,
  props: {
    id: { type: String, required: false, default: "test" },
    type: { type: String, required: false, default: "default" },
    buttonType: { type: String, required: false, default: "button" },
    size: { type: String, required: false, default: "md" },
    icon: { type: String, required: false, default: null },
    iconSize: { type: String, required: false, default: null }, // this should defualt to prop `size` if not present
    iconColor: { type: String, required: false, default: null },
    selected: { type: Boolean, required: false, default: false },
    iconRight: Boolean,
    shadow: { type: Boolean, required: false, default: false },
    disabled: Boolean,
    loading: Boolean,
    label: { type: String, default: "" },
    to: { type: String, default: null },
    toExternal: { type: String, default: null },
    center: { type: Boolean, required: false, default: true },
  },
  computed: {
    listeners() {
      return {
        ...this.$listeners,
      };
    },
    showIcon() {
      return this.icon && !this.loading;
    },
  },
  methods: {
    routeTo() {
      if (this.toExternal) openInNewTab(this.toExternal);
      if (this.to) this.$router.push(this.to);
    },
  },
};
</script>

<style lang="scss" scoped>
.base-button {
  border: none;
  box-sizing: border-box;
  border-radius: 5px;
  padding: 6px 10px;
  margin: 2px;
  background-color: #f5f5f5;
  border: 1px solid #f5f5f5;
  font-size: 12px;
  cursor: pointer;
  display: inline-flex;
  flex-flow: row nowrap;
  align-items: center;
  box-shadow: 2px 4px 8px rgba(0, 0, 0, 0.05);
  min-height: 30px;
  &:hover {
    background-color: #dcdcdc;
    border: 1px solid #dcdcdc;
  }
  &.selected {
    background-color: darken(#f5f5f5, 10%);
  }
  &.white {
    border: 1px solid #dddddd;
    background-color: #fff;
  }
  &.white:hover {
    background-color: darken(#f5f5f5, 10%);
  }
  &.white.selected {
    background-color: darken(#f5f5f5, 10%);
  }
  &.black {
    background-color: #000;
    color: #fff;
    border: 1px solid #444444;
  }
  &.black:hover {
    background-color: darken(#f5f5f5, 10%);
  }
  &.primary {
    border: 1px solid #6ab4e4;
    font-weight: 500;
    color: #fff;
    background-color: #6ab4e4;
  }
  &.primary:hover {
    background: lighten(#6ab4e4, 10%);
    border: 1px solid lighten(#6ab4e4, 10%);
  }
  &.primary-dark {
    border: 1px solid #60a2ce;
    font-weight: 500;
    color: #fff;
    background-color: #60a2ce;
  }
  &.primary-dark:hover {
    border: 1px solid #6ab4e4;
    font-weight: 500;
    color: #fff;
    background-color: #6ab4e4;
  }
  &.success {
    font-weight: 500;
    color: #fff;
    background-color: #89c541;
    border: 1px solid #89c541;
  }
  &.success:hover {
    background: lighten(#89c541, 10%);
    border: 1px solid lighten(#89c541, 10%);
  }

  &.off-primary {
    color: white;
    background-color: #60a2ce;
    border: 1px solid #60a2ce;
  }

  &.off-primary:hover {
    background-color: #73abd1;
    border: 1px solid #73abd1;
  }

  &.disabled {
    pointer-events: none;
    opacity: 0.7;
    cursor: not-allowed;
  }

  &.new {
    color: #fff;
    font-weight: 500;
    background: #89c541;
    border: 1px solid #89c541;
  }
  &.new:hover {
    background: lighten(#89c541, 10%);
    border: 1px solid lighten(#89c541, 10%);
  }

  &.xl {
    padding: 13px 20px;
  }
  &.lg {
    padding: 12px 14px;
  }
  &.md {
    font-size: 12px;
    padding: 8px 8px;
    max-height: 30px;
  }
  &.sm {
    font-size: 12px;
    padding: 6px 8px;
  }
  &.xsm {
    font-size: 10px;
    min-height: 15px;
  }
  &.full {
    font-size: 14px;
    padding: 8px 12px;
    width: 100%;
  }
  &.full-width {
    font-size: 12px;
    padding: 8px 8px;
    max-height: 30px;
    width: 100%;
  }
  &.shadow {
    box-shadow: 1px 4px 7px rgba(0, 0, 0, 0.25);
  }
}

.base-button-text {
  white-space: nowrap;
  pointer-events: none;
  flex: 1;
  &.center {
    flex: 1;
    text-align: center;
  }
}
</style>
