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
        <v-form lazy-validation>
          <v-layout row justify-center>
            <v-flex xs6>
              <section class="profile-section">
                <h1 class="title my-2">Profile</h1>
                <h2 class="subheading my-3">
                  Some info may be visible to other people using centrade
                  service.
                </h2>
                <v-text-field label="First Name" />
                <v-text-field label="Middle Name" />
                <v-text-field label="Last Name" />
                <v-text-field label="Gender" />
                <v-text-field label="Date of birth" />
              </section>
              <section class="profile-section">
                <h1 class="title my-2">Contact info</h1>
                <v-text-field label="E-mail" />
                <v-text-field label="Phone" />
              </section>
              <section class="profile-section">
                <h1 class="title my-2">Business info</h1>
                <v-text-field label="ABN" />
                <v-text-field label="License" />
              </section>

              <section class="profile-section">
                <h1 class="title my-2">Address</h1>
                <v-text-field label="Address 1" />
                <v-text-field label="Address 2" />
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
        </v-form>
      </article>
    </section>
  </v-container>
</template>
<script>
export default {}
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
