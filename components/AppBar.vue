<template>
  <v-app-bar fixed app dark clipped-left color="#384596">
    <v-app-bar-nav-icon v-if="$auth.loggedIn" />
    <v-toolbar-title>
      <nuxt-link to="/">
        <v-img src="/images/logo.png" width="120" />
      </nuxt-link>
    </v-toolbar-title>
    <v-spacer />

    <!-- Authenticated -->
    <template v-if="$auth.loggedIn">
      <v-menu
        origin="center center"
        offset-y
        :nudge-bottom="10"
        transition="scale-transition"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-btn v-bind="attrs" text v-on="on">
            <v-icon left>
              person
            </v-icon>
            {{ $auth.user.name }}
          </v-btn>
        </template>
        <v-list class="pa-0">
          <v-list-item
            v-for="(item, index) in account_items"
            :key="index"
            ripple="ripple"
            :disabled="item.disabled"
            :target="item.target"
            rel="noopener"
            @click="accountMenuItemClicked(item.action)"
          >
            <v-list-item-action>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-item-action>
            <v-list-item-title>
              {{ item.title }}
            </v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </template>

    <!-- Guest -->
    <template v-else>
      <v-btn text to="/register">
        {{ 'Register' }}
      </v-btn>
      <v-btn text to="/login">
        {{ 'login' }}
      </v-btn>
    </template>
  </v-app-bar>
</template>

<script>
export default {
  data() {
    return {
      busy: false,
      account_items: [
        {
          icon: 'account_circle',
          href: '#',
          title: 'Account',
          action: 'profile'
        },
        {
          icon: 'fullscreen_exit',
          href: '#',
          title: 'Logout',
          action: 'logout'
        }
      ],
      appName: 'Centrade',
      drawer: false
    }
  },
  methods: {
    async logout() {
      await this.$auth.logout()
      // Redirect to login.
      this.$router.push({ name: 'login' })
    },
    accountMenuItemClicked(action) {
      switch (action) {
        case 'profile':
          this.$router.push({ name: 'account-profile' })
          break
        case 'logout':
          this.logout()
          break
      }
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
