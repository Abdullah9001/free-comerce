<template>
  <v-card rounded="lg" class="pa-md-10 pa-5 text-center" color="primary" dark>
    <h2 class="text-md-h3">Newsletter</h2>
    <p class="text-md-h6 mt-5">Subscribe to receive discount & more</p>
    <v-sheet color="transparent" class="mx-auto" max-width="400">
      <v-text-field
        label="Email"
        type="email"
        outlined
        v-model="email"
      ></v-text-field>
      <v-btn @click="done" outlined min-height="50" block>Subscribe</v-btn>
    </v-sheet>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      email: null,
    }
  },
  methods: {
    async done() {
      await this.$swal({
        title: 'Thank you for subscribing',
        icon: 'success',
        allowOutsideClick: false,
        allowEscapeKey: false,
        timer: 3000,
        timerProgressBar: true,
        showConfirmButton: false,
        text: 'You will be notified when we have a deal or items on sale.',
      })
    },
  },
}
</script>

<style></style>
