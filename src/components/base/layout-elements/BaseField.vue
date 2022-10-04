<template>
  <div class="base-field">
    <div style="width: 100%">
      <slot />
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
.base-field {
  display: inline-block;
  width: 100%;
  margin-bottom: 15px;

  &.base-input-error {
    input,
    select {
      border: 1px solid red;
    }
  }

  .label-helper {
    padding-bottom: 5px;
    min-height: 10px;
    label {
      font-weight: 400;
    }
  }

  .base-error-message {
    font-size: 12px;
    color: red;
    padding: 5px 0px;
  }

  .require {
    color: #6ab4e4;
  }

  .bold-label {
    font-weight: 500;
  }

  .helper {
    display: block;
    padding-bottom: 5px;
    color: #666666;
  }

  input {
    width: 100%;
    background: #ffffff;
    // border: 1px solid #DDDDDD;
    box-sizing: border-box;
    border-radius: 5px;
    padding: 8px;
    font-size: 12px;
    max-height: 30px;

    &.base-input-error {
      border: 1px solid red;
    }

    &:focus {
      outline: none;
      border: 1px solid #6ab4e4;
    }
  }

  .horizontal {
    display: flex;
    flex-flow: row nowrap;

    .input {
      flex: 2;
      display: flex;
    }

    .label-helper {
      flex: 1;
      text-align: right;
      padding-top: 10px;
      padding-right: 10px;
    }

    &.small {
      flex-flow: column nowrap;
      align-items: stretch;

      .label-helper {
        text-align: left;
        padding: 0;
      }
    }
  }
}
</style>
