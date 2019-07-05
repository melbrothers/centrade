<template>
  <v-form @submit.prevent="login">
    <v-card class="elevation-12">
      <v-toolbar dark color="primary">
        <v-toolbar-title>Login form</v-toolbar-title>
        <v-spacer />
      </v-toolbar>
      <v-card-text>
        <v-text-field
          v-model="email"
          prepend-icon="email"
          label="Login"
          type="text"
        />
        <v-text-field
          id="password"
          v-model="password"
          prepend-icon="lock"
          label="Password"
          type="password"
        />
      </v-card-text>
      <v-card-actions>
        <v-spacer />
        <v-btn color="primary" type="submit">
          Login
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-form>
</template>
<script>
export default {
  data() {
    return {
      email: 'zlxjackie@hotmail.com',
      password: 'secretsecret',
      error: null
    }
  },
  methods: {
    async login() {
      try {
        await this.$auth.loginWith('local', {
          data: {
            email: this.email,
            password: this.password
          }
        })

        this.$router.push('/')
      } catch (e) {
        this.error = e.response.data.message
      }
    }
  }
}
</script>
