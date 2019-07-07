<template>
  <form @submit.prevent="register">
    <v-card class="elevation-12">
      <v-toolbar dark color="primary">
        <v-toolbar-title>Register Form</v-toolbar-title>
        <v-spacer />
      </v-toolbar>
      <v-card-text>
        <v-text-field
          v-model="email"
          v-validate="'required|email'"
          prepend-icon="email"
          label="Email"
          data-vv-name="email"
          type="text"
          autofocus
          :error-messages="errors.collect('email')"
        />
        <v-text-field
          v-model="password"
          v-validate="'required'"
          prepend-icon="lock"
          label="Password"
          type="password"
          data-vv-name="password"
          :error-messages="errors.collect('password')"
        />
        <v-text-field
          v-model="passwordConfirmation"
          v-validate="'required'"
          prepend-icon="lock"
          label="Confrim Password"
          type="password"
          data-vv-name="password_confirmation"
          :error-messages="errors.collect('password_confirmation')"
        />
      </v-card-text>
      <v-card-actions>
        <v-spacer />
        <v-btn color="primary" type="submit">
          Register
        </v-btn>
      </v-card-actions>
    </v-card>
  </form>
</template>
<script>
export default {
  data() {
    return {
      email: '',
      password: 'secretsecret',
      passwordConfirmation: 'secretsecret'
    }
  },
  methods: {
    async register() {
      try {
        const result = await this.$validator.validate()
        if (!result) {
          return
        }
        await this.$axios.post('register', {
          email: this.email,
          password: this.password,
          password_confirmation: this.passwordConfirmation
        })
        await this.$auth.loginWith('local', {
          data: {
            email: this.email,
            password: this.password
          }
        })

        this.$router.push('/')
      } catch (e) {
        this.$setLaravelValidationErrorsFromResponse(e.response.data)
      }
    }
  }
}
</script>
