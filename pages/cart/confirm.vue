<template>
  <div>
    <div v-if="$store.state.cart.cart.length == 0" class="text-center">
      <p>No Item Yet. Keep Shopping.</p>
    </div>
    <v-container>
      <div class="mb-3" v-if="$store.state.cart.cart.length > 0">
        <v-btn nuxt to="/cart" min-height="45" min-width="150" depressed
          >Back</v-btn
        >
      </div>
      <v-form lazy-validation ref="form" class="mt-10">
        <p class="font-weight-bold">Personal & Delivery</p>
        <v-row>
          <v-col cols="12" md="4">
            <v-text-field v-model="email" outlined label="Email" type="email">
            </v-text-field>
          </v-col>

          <v-col cols="12" md="4">
            <v-text-field v-model="name" outlined label="Full Name" type="name">
            </v-text-field>
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field v-model="phone" outlined label="Phone" type="tel">
            </v-text-field>
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field
              v-model="address"
              outlined
              label="Address"
              type="text"
            >
            </v-text-field>
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field v-model="city" outlined label="City" type="text">
            </v-text-field>
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field v-model="contry" outlined label="Contry" type="text">
            </v-text-field>
          </v-col>
        </v-row>
        <p class="font-weight-bold">Credit Card</p>
        <v-row>
          <v-col cols="12" md="12">
            <v-text-field v-model="cc" outlined label="Credit Card Number">
            </v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <v-text-field v-model="expdata" outlined label="Exp Data">
            </v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <v-text-field v-model="cvv" outlined label="Security code/CVV">
            </v-text-field>
          </v-col>
        </v-row>
      </v-form>
      <v-btn @click="proccess" min-height="45" min-width="150" color="primary"
        >Complete</v-btn
      >
    </v-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: null,
      name: null,
      pgone: null,
      address: null,
      city: null,
      country: null,
      cc: '424242424242',
      expdata: '06/15',
      cvv: '123',
    }
  },
  methods: {
    async proccess() {
      if ((this.email = '')) return
      await this.$swal({
        title: 'Proceessing your order',
        icon: 'info',
        allowEscapeKey: false,
        allowOutsideClick: false,
        timer: 3000,
        timerProgressBar: true,
        text: 'Please Wait',
        showConfirmButton: false,
      })
      await this.$swal({
        title: 'Order Complete',
        icon: 'success',
        allowEscapeKey: false,
        allowOutsideClick: false,
        timer: 4000,
        timerProgressBar: true,
        text: 'Thank You So Much ❤',
        showConfirmButton: false,
      })
      //Remove items from cart
      this.$store.commit('cart/ClearCart')
      this.$router.push('/')
    },
  },
}
</script>

<style></style>
