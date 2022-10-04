<template>
  <span>
    <font-awesome-icon
      :icon="[type, icon]"
      class="base-icon"
      :class="color"
      v-bind="$attrs"
      v-on="listeners"
    />
  </span>
</template>

<script>
export default {
  inheritAttrs: false,
  props: {
    icon: { type: String, default: "account" },
    color: { type: String, default: "blue" },
    type: { type: String, default: "fas" },
  },
  computed: {
    listeners() {
      return {
        ...this.$listeners,
        input: (event) => {
          this.$emit("input", event.target.value);
        },
      };
    },
  },
};
</script>

<style lang="scss" scoped>
.base-icon {
  cursor: pointer;

  &.white {
    color: white;
  }
  &.lightblack {
    color: #343434;
  }
}
</style>