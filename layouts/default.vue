<template>
  <v-app light>
    <AppBar :drawer="drawer" @toggleDrawer="drawer = !drawer" />
    <v-content>
      <v-container fluid>
        <transition name="page" mode="out-in">
          <nuxt />
        </transition>
      </v-container>
    </v-content>
  </v-app>
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
