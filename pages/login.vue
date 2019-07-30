<template>
  <v-layout class="pa-0" row wrap align-center justify-center>
    <v-flex xs4>
      <Login />
    </v-flex>
  </v-layout>
</template>
<script>
import Login from '~/components/Login.vue'

export default {
  components: {
    Login
  }
}
</script>
