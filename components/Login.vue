<template>
  <v-card class="elevation-12">
    <v-toolbar dark color="primary">
      <v-toolbar-title>Login form</v-toolbar-title>
      <v-spacer />
    </v-toolbar>
    <v-card-text>
      <v-form>
        <v-text-field
          prepend-icon="person"
          name="login"
          label="Login"
          type="text"
        />
        <v-text-field
          id="password"
          prepend-icon="lock"
          name="password"
          label="Password"
          type="password"
        />
      </v-form>
    </v-card-text>
    <v-card-actions>
      <v-spacer />
      <v-btn color="primary" @click="login">
        Login
      </v-btn>
    </v-card-actions>
  </v-card>
</template>
<script>
export default {
  methods: {
    async login() {
      await this.$auth.loginWith('local', {
        data: {
          email: 'this.email',
          password: 'this.password'
        }
      })
    }
  }
}
</script>
