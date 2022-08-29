<template>
  <v-carousel height="100vh" hide-delimiter-background>
    <template #prev="{ attrs, on }">
      <v-btn fab color="transparent" depressed v-bind="attrs" v-on="on">
        <v-icon size="20">mdi-arrow-left</v-icon>
      </v-btn>
    </template>
    <template #next="{ attrs, on }">
      <v-btn fab color="transparent" depressed v-bind="attrs" v-on="on">
        <v-icon size="20">mdi-arrow-right</v-icon>
      </v-btn>
    </template>
    <v-carousel-item v-for="(p, i) in sale_items" :key="`saleItem-${i}`">
      <v-img height="100vh" :src="p.image">
        <v-container class="fill-height">
          <v-row dense align="center">
            <v-col md="7">
              <div
                style="background-color: rgba(255, 255, 255, 0.8)"
                class="pa-md-10 pa-5 rounded-lg black--text text-center text-md-left"
              >
                <h2 class="text-md-h3 text-h5">{{ p.name }}</h2>
                <p class="text-md-h5 text-subtitle-1 primary--text mt-5">
                  {{ $formatMoney(p.price) }}
                </p>
                <p class="text-md-body-2 mb-7">{{ p.description }}</p>
                <v-btn
                  nuxt
                  :to="`/products/${p.id}`"
                  depressed
                  color="primary"
                  class="text-capitalize"
                  min-height="40"
                  >Check In Out</v-btn
                >
              </div>
            </v-col>
          </v-row>
        </v-container>
      </v-img>
    </v-carousel-item>
  </v-carousel>
</template>

<script>
export default {
  props: {
    sale_items: Array,
  },
}
</script>

<style></style>
