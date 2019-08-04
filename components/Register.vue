<template>
  <form @submit.prevent="register">
    <v-card class="elevation-12">
      <v-toolbar dark color="primary">
        <v-toolbar-title>Register</v-toolbar-title>
        <v-spacer />
      </v-toolbar>
      <v-card-text>
        <v-text-field
          v-model="abn"
          v-validate="'required|numeric'"
          prepend-icon="business"
          label="ABN"
          data-vv-name="abn"
          type="text"
          autofocus
          :error-messages="errors.collect('abn')"
        />
        <v-text-field
          v-model="businessName"
          v-validate="'required'"
          prepend-icon="contact_mail"
          label="Business Name"
          data-vv-name="businessName"
          type="text"
          autofocus
          :error-messages="errors.collect('businessName')"
        />
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
      abn: '',
      businessName: '',
      email: '',
      password: '',
      passwordConfirmation: ''
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
          abn: this.abn,
          businessName: this.businessName,
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

        this.$router.push('/account/profile')
      } catch (e) {
        this.$setLaravelValidationErrorsFromResponse(e.response.data)
      }
    }
  }
}
</script>
