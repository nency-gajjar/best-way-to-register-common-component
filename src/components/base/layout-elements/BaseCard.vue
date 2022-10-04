<template>
  <div class="base-card-wrapper">
    <div
      :class="['base-card', size, color, { 'base-card-shadow': shadow }]"
      v-bind="$attrs"
      v-on="$listeners"
    >
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  inheritAttrs: false,
  props: {
    shadow: { type: Boolean, required: false, default: false },
    size: {
      type: String,
      default: "is-full",
      validator: function (value) {
        return ["is-small", "is-full"].indexOf(value) !== -1;
      },
    },
    color: {
      type: String,
      default: "white",
      validator: function (value) {
        return ["gray", "white"].indexOf(value) !== -1;
      },
    },
  },
};
</script>

<style lang="scss" scoped>
.base-card-wrapper {
  background: transparent;
  width: 100%;

  .base-card-shadow {
    box-shadow: 2px 4px 12px rgba(0, 0, 0, 0.05);
    border-radius: 6px;
  }

  .base-card {
    padding: 20px;
    border-radius: 8px;
    border: 1px solid #dddddd;
    width: 100%;
    background: #fff;

    &.gray {
      background: #dddddd;
    }
    &.is-small {
      max-width: 500px;
      display: inline-block;
    }
    &.is-full {
      min-height: 100%;
      width: 100%;
    }
  }
}
@media screen and (max-width: 767px) {
  .d-flex-none .base-card.is-full.white {
    display: block;
    width: 100%;
    overflow-x: auto;
    -webkit-overflow-scrolling: touch;
  }
}
</style>