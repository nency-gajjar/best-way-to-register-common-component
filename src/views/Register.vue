<template>
  <div>
    <h1>Register</h1>
    <BaseCard size="is-small">
      <BaseInput
        v-model="firstName"
        type="text"
        placeholder="First Name"
        required
        icon="user"
      />
      <BaseInput
        v-model="lastName"
        type="text"
        placeholder="Last Name"
        required
        icon="user"
      />
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
        label="Register"
        button-type="submit"
      />
    </BaseCard>
  </div>
</template>

<script>
export default {
  data() {
    return {
      firstName: "",
      lastName: "",
      email: "",
      password: "",
    };
  },
};
</script>
