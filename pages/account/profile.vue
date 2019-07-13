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
                <v-select :items="titles" label="Title" />
                <v-text-field label="First Name" />
                <v-text-field label="Last Name" />
                <v-select :items="states" label="Gender" />
                <v-menu
                  v-model="menu2"
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
                      v-model="date"
                      label="Picker without buttons"
                      prepend-icon="event"
                      readonly
                      v-on="on"
                    />
                  </template>
                  <v-date-picker
                    v-model="date"
                    no-title
                    @input="menu2 = false"
                  />
                </v-menu>
              </section>
              <section class="profile-section">
                <h1 class="title my-2">
                  Contact info
                </h1>
                <v-text-field label="Mobile Phone" />
                <v-text-field label="Landline" />
              </section>
              <section class="profile-section">
                <h1 class="title my-2">
                  Business info
                </h1>
                <v-text-field label="ABN" />
                <v-text-field label="License" />
              </section>

              <section class="profile-section">
                <h1 class="title my-2">
                  Address
                </h1>
                <v-text-field label="Address 1" />
                <v-text-field label="Address 2" />
                <v-text-field label="Suburb" />
                <v-select :items="states" label="State" />
                <v-text-field label="Postcode" />
              </section>
            </v-flex>
          </v-layout>
          <v-layout column>
            <v-flex xs6 align-self-center>
              <v-btn class="save-btn mx-2" color="primary">
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
      profile: {
        firstName: '',
        lastName: '',
        address1: '',
        address2: '',
        suburb: '',
        postcode: ''
      },
      titles: ['Mr', 'Mrs', 'Ms'],
      states: ['NSW', 'ACT', 'VIC', 'SA', 'NT', 'TAS'],
      date: new Date().toISOString().substr(0, 10),
      modal: false,
      menu2: false,
      genders: ['Male', 'Female']
    }
  },
  methods: {
    async updateProfile() {
      try {
      } catch (e) {}
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
