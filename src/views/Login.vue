<template>
  <div>
    <h1>Login</h1>
    <BaseCard size="is-small">
      <BaseInput
        v-model="email"
        type="email"
        placeholder="e.g. bobsmith@gmail.com"
        required
        icon="envelope"
      />
      <BaseInput
        v-model="password"
        type="password"
        placeholder="*******"
        required
        icon="lock"
      />
      <BaseButton
        size="full"
        type="primary"
        label="Login"
        button-type="submit"
      />
    </BaseCard>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
    };
  },
};
</script>
