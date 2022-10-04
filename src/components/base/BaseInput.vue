<template>
  <BaseField :class="['base-input', size]" v-bind="$attrs">
    <input
      ref="baseinput"
      :class="{ 'search-box': searchBox, rounded: rounded }"
      v-bind="$attrs"
      :value="value"
      :disabled="disabled || loading"
      v-on="listeners"
      @blur="showSearchTip = false"
    />
    <BaseIcon :icon="icon" class="input-icon" />
  </BaseField>
</template>

<script>
export default {
  inheritAttrs: false,
  props: {
    icon: { type: String, required: false, default: null },
    searchBox: Boolean,
    value: { default: null },
    size: {
      type: String,
      default: "is-full",
      validator: function (value) {
        return ["is-half", "is-full"].indexOf(value) !== -1;
      },
    },
    rounded: {
      type: Boolean,
      default: true,
    },
    debounce: {
      type: Boolean,
      default: false,
    },
    debounceTime: {
      type: Number,
      default: 800,
    },
    loading: {
      type: Boolean,
      default: false,
    },
    disabled: {
      type: Boolean,
      default: false,
    },
  },
  computed: {
    listeners() {
      const listeners = { ...this.$listeners };
      const input = (event) => {
        this.$emit("input", event.target.value);
      };
      listeners.input = this.debounce
        ? _.debounce(input, this.debounceTime)
        : input;
      return listeners;
    },
  },
};
</script>

<style lang="scss" scoped>
.input-icon {
  position: relative;
  right: 10px;
  top: 7px;
  color: #6ab4e4;
}
.base-input {
  position: relative;
  display: inline-block;
  width: 100%;
  .helper-text {
    display: block;
    font-size: 12px;
    margin-top: 5px;
    margin-bottom: 5px;
    position: relative;
  }
  span {
    position: absolute;
  }
  input {
    width: 100%;
    background: #ffffff;
    border: 1px solid #dddddd;
    box-sizing: border-box;
    border-radius: 5px;
    padding: 8px;
    font-size: 12px;
    max-height: 30px;
    &[disabled="disabled"] {
      background: #f5f5f5;
      color: #999999;
      cursor: not-allowed;
    }
  }
  .search-box {
    border: 1px solid #dddddd;
    padding: 6px 22px 6px 12px;
    font-size: 12px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    &.rounded {
      border-radius: 50px 0 0 50px;
    }
  }
  input:focus {
    outline: none;
    border: 1px solid #6ab4e4;
  }
  input::placeholder {
    color: #999999;
    &.search-box {
      color: #444444;
    }
  }
  .base-error-message {
    font-size: 12px;
    color: #ed0d21;
    padding: 5px 0px;
  }
}
.is-half {
  width: 49%;
}
.is-full {
  width: 100%;
}
.icon {
  padding: 7px 9px 7px 9px;
  right: -28px;
  color: white;
  background: #444444;
  border-radius: 0 50px 50px 0px;
  cursor: pointer;
  &:hover {
    background: lighten(#444444, 10%);
  }
}
</style>