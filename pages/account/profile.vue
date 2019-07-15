<template>
  <v-container fluid>
    <header>
      <h1 class="text-xs-center display-1 my-2">
        Personal Info
      </h1>
      <h2 class="subheading text-xs-center my-3">
        Basic info, like your name and photo, that you use on centrade services
      </h2>
    </header>
    <section>
      <article>
        <form @submit.prevent="updateProfile">
          <v-layout row justify-center>
            <v-flex xs6>
              <section class="profile-section">
                <h1 class="title my-2">
                  Profile
                </h1>
                <h2 class="subheading my-3">
                  Some info may be visible to other people using centrade
                  service.
                </h2>
                <v-select
                  v-model="profile.title"
                  v-validate="'required'"
                  data-vv-name="title"
                  :error-messages="errors.collect('title')"
                  :items="titles"
                  label="Title"
                />
                <v-text-field
                  v-model="profile.firstName"
                  v-validate="'required|alpha'"
                  label="First Name"
                  data-vv-name="firstName"
                  :error-messages="errors.collect('firstName')"
                />
                <v-text-field
                  v-model="profile.lastName"
                  v-validate="'required|alpha'"
                  label="Last Name"
                  data-vv-name="lastName"
                  :error-messages="errors.collect('lastName')"
                />
                <v-select
                  v-model="profile.gender"
                  v-validate="'required'"
                  :items="genders"
                  label="Gender"
                  data-vv-name="gender"
                  :error-messages="errors.collect('gender')"
                />
                <v-menu
                  v-model="menu"
                  :close-on-content-click="false"
                  :nudge-right="40"
                  lazy
                  transition="scale-transition"
                  offset-y
                  full-width
                  min-width="290px"
                >
                  <template v-slot:activator="{ on }">
                    <v-text-field
                      v-model="profile.dob"
                      label="Date of Birth"
                      prepend-icon="event"
                      readonly
                      v-on="on"
                    />
                  </template>
                  <v-date-picker
                    v-model="profile.dob"
                    no-title
                    @input="menu = false"
                  />
                </v-menu>
              </section>
              <section class="profile-section">
                <h1 class="title my-2">
                  Contact info
                </h1>
                <v-text-field
                  v-model="profile.mobile"
                  v-validate="'required'"
                  data-vv-name="mobile"
                  :error-messages="errors.collect('mobile')"
                  label="Mobile Phone"
                />
                <v-text-field
                  v-model="profile.landline"
                  v-validate="'required'"
                  data-vv-name="landline"
                  :error-messages="errors.collect('landline')"
                  label="Landline"
                />
              </section>
              <section class="profile-section">
                <h1 class="title my-2">
                  Business info
                </h1>
                <v-text-field
                  v-model="profile.abn"
                  v-validate="'required|numeric'"
                  data-vv-name="abn"
                  :error-messages="errors.collect('abn')"
                  label="ABN"
                />
                <v-text-field
                  v-model="profile.licence"
                  v-validate="'numeric'"
                  data-vv-name="licence"
                  :error-messages="errors.collect('licence')"
                  label="Licence"
                />
              </section>

              <section class="profile-section">
                <h1 class="title my-2">
                  Address
                </h1>
                <v-text-field
                  v-model="profile.address1"
                  v-validate="'required'"
                  data-vv-name="address1"
                  :error-messages="errors.collect('address1')"
                  label="Address 1"
                />
                <v-text-field
                  v-model="profile.address2"
                  v-validate="'alpha_dash'"
                  data-vv-name="address2"
                  :error-messages="errors.collect('address2')"
                  label="Address 2"
                />
                <v-text-field
                  v-model="profile.suburb"
                  v-validate="'required'"
                  data-vv-name="suburb"
                  :error-messages="errors.collect('suburb')"
                  label="Suburb"
                />
                <v-select
                  v-model="profile.state"
                  v-validate="'required'"
                  :items="states"
                  data-vv-name="state"
                  :error-messages="errors.collect('state')"
                  label="State"
                />
                <v-text-field
                  v-model="profile.postcode"
                  v-validate="'required'"
                  data-vv-name="postcode"
                  :error-messages="errors.collect('postcode')"
                  label="Postcode"
                />
              </section>
            </v-flex>
          </v-layout>
          <v-layout column>
            <v-flex xs6 align-self-center>
              <v-btn class="save-btn mx-2" color="primary" type="submit">
                Save
              </v-btn>
            </v-flex>
          </v-layout>
        </form>
      </article>
    </section>
  </v-container>
</template>
<script>
export default {
  data() {
    return {
      titles: ['Mr', 'Mrs', 'Ms'],
      states: ['NSW', 'ACT', 'VIC', 'SA', 'NT', 'TAS'],
      modal: false,
      menu: false,
      genders: ['Male', 'Female']
    }
  },
  async asyncData({ app }) {
    const { data } = await app.$axios.get('user/profile')
    console.log(data.data)
    return { profile: data.data }
  },
  methods: {
    async updateProfile() {
      try {
        const result = await this.$validator.validate()
        if (!result) {
          return
        }

        await this.$axios.post('/user/profile', this.profile)

        this.$dialog.message.success('Profile Updated', {
          position: 'top-right'
        })
      } catch (e) {
        this.$setLaravelValidationErrorsFromResponse(e.response.data)
      }
    }
  }
}
</script>
<style scoped lang="stylus">
h1 {
  color: #202124;
}

h2 {
  color: #5f6368;
}

.profile-section {
  border: 1px solid #dadce0;
  border-radius: 15px;
  padding: 10px 20px;
  margin: 20px;
}

.save-btn {
  width: 30vw;
}
</style>
