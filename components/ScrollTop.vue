<template>
  <v-fab-transition>
    <v-btn
      fixed
      right
      bottom
      fab
      @click="goUp"
      color="primary"
      v-scroll="checkScroll"
      v-show="showFab"
      ><v-icon>mdi-chevron-up</v-icon></v-btn
    >
  </v-fab-transition>
</template>

<script>
export default {
  data() {
    return {
      showFab: false,
    }
  },
  methods: {
    checkScroll() {
      const h = window.scrollY
      if (h > 300) {
        this.showFab = true
      } else {
        this.showFab = false
      }
    },
    goUp() {
      this.$vuetify.goTo(0, {
        duration: 1000,
      })
    },
  },
}
</script>

<style></style>
