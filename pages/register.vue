<template>
  <v-container fluid>
    <v-layout class="pa-0" row wrap align-center justify-center>
      <v-flex xs4>
        <Register />
      </v-flex>
    </v-layout>
  </v-container>
</template>
<script>
import Register from '~/components/Register.vue'

export default {
  components: {
    Register
  }
}
</script>
