<template>
  <v-app
    dark
    :style="{ background: $vuetify.theme.dark ? '#0a0514' : 'white' }"
  >
    <v-main>
      <Navber />
      <Nuxt />
      <Footer />
      <ScrollTop />
    </v-main>
  </v-app>
</template>

<script>
export default {}
</script>
