<template>
  <form @submit.prevent="login">
    <v-card class="elevation-12">
      <v-toolbar dark color="primary">
        <v-toolbar-title>Login form</v-toolbar-title>
        <v-spacer />
      </v-toolbar>
      <v-card-text>
        <v-text-field
          v-model="email"
          v-validate="'required|email'"
          prepend-icon="email"
          label="Email"
          type="text"
          data-vv-name="email"
          autofocus
          :error-messages="errors.collect('email')"
        />
        <v-text-field
          id="password"
          v-model="password"
          v-validate="'required'"
          prepend-icon="lock"
          label="Password"
          type="password"
          data-vv-name="password"
          :error-messages="errors.collect('password')"
        />
      </v-card-text>
      <v-card-actions>
        <v-spacer />
        <v-btn color="primary" type="submit">
          Login
        </v-btn>
      </v-card-actions>
    </v-card>
  </form>
</template>
<script>
export default {
  data() {
    return {
      email: 'zlxjackie@hotmail.com',
      password: 'secretsecret'
    }
  },
  methods: {
    async login() {
      try {
        const result = await this.$validator.validate()
        if (!result) {
          return
        }

        await this.$auth.loginWith('local', {
          data: {
            email: this.email,
            password: this.password
          }
        })

        this.$router.push('/account/profile')
      } catch (e) {
        this.$setLaravelValidationErrorsFromResponse(e.response.data)
      }
    }
  }
}
</script>
