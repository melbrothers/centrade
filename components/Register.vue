<template>
  <v-form @submit.prevent="register">
    <v-card class="elevation-12">
      <v-toolbar dark color="primary">
        <v-toolbar-title>Register Form</v-toolbar-title>
        <v-spacer />
      </v-toolbar>
      <v-card-text>
        <v-text-field
          v-model="email"
          prepend-icon="email"
          label="Email"
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
          Register
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
    async register() {
      try {
        await this.$axios.post('register', {
          email: this.email,
          password: this.password
        })

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
