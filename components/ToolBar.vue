<template>
  <v-toolbar fixed app dark clipped-left color="#384596">
    <v-toolbar-side-icon
      v-if="$auth.$state.loggedIn"
      @click.stop="toggleDrawer"
    />
    <v-toolbar-title>
      <nuxt-link to="/" class="white--text">
        <img src="/images/logo.png" height="50" />
      </nuxt-link>
    </v-toolbar-title>
    <v-spacer />

    <!-- Authenticated -->
    <template v-if="$auth.$state.loggedIn">
      <v-menu
        origin="center center"
        offset-y
        :nudge-bottom="10"
        transition="scale-transition"
      >
        <v-btn slot="activator" flat>
          <v-icon left>
            person
          </v-icon>
          {{ $auth.$state.authUser.name }}
        </v-btn>
        <v-list class="pa-0">
          <v-list-tile
            v-for="(item, index) in account_items"
            :key="index"
            ripple="ripple"
            :disabled="item.disabled"
            :target="item.target"
            rel="noopener"
            @click="accountMenuItemClicked(item.action)"
          >
            <v-list-tile-action v-if="item.icon">
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title>{{ item.title }}</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        </v-list>
      </v-menu>
    </template>

    <!-- Guest -->
    <template v-else>
      <v-btn flat to="/about">
        {{ 'About' }}
      </v-btn>
      <v-btn flat @click="showLogin">
        {{ 'login' }}
      </v-btn>
    </template>
  </v-toolbar>
</template>

<script>
export default {
  data() {
    return {
      busy: false,
      account_items: [],
      appName: 'Centrade',
      drawer: false
    }
  }
  //   computed: mapGetters({
  //     user: 'authUser',
  //     authenticated: 'authCheck'
  //   }),
  //     toggleDrawer () {
  //       this.$emit('toggleDrawer')
  //     }
  //   methods: {
  //     async logout () {
  //       this.busy = true
  //       if (this.drawer) {
  //         this.toggleDrawer()
  //       }
  //       // Log out the user.
  //       await this.$store.dispatch('logout')
  //       this.busy = false
  //       // Redirect to login.
  //       this.$router.push({ name: 'login' })
  //     },
  //     accountMenuItemClicked(action) {
  //       switch (action) {
  //         case 'profile':
  //           this.$router.push({ name: 'settings.profile' })
  //           break;
  //         case 'logout':
  //           this.logout();
  //           break;
  //       }
  //     },
  //   }
}
</script>

<style lang="stylus" scoped>
.toolbar__title .router-link-active {
  text-decoration: none;
}
</style>
