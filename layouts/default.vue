<template>
  <transition name="page" mode="out-in">
    <v-app light>
      <AppBar :drawer="drawer" @toggleDrawer="drawer = !drawer" />
      <v-content>
        <v-container fluid>
          <nuxt />
        </v-container>
      </v-content>
    </v-app>
  </transition>
</template>

<script>
import AppBar from '~/components/AppBar.vue'

export default {
  components: {
    AppBar
  },
  data() {
    return {
      drawer: false
    }
  }
}
</script>
