<template>
  <div>
    <v-container>
      <v-row dense>
        <v-col md="3">
          <div>
            <v-text-field
              v-model="search"
              prepend-inner-icon="mdi-magnify"
              outlined
              clearable
              placeholder="Search"
            >
            </v-text-field>
            <v-list
              subheader
              color="transparent"
              v-if="$vuetify.breakpoint.mdAndUp"
            >
              <v-subheader>Categories</v-subheader>
              <v-list-item
                v-for="(c, i) in categories"
                :key="`category${i}`"
                @click="selectCategory(c.name)"
                link
                ><v-list-item-avatar>
                  <v-img :src="c.image"></v-img>
                </v-list-item-avatar>
                <v-list-item-content>
                  <v-list-item-title>
                    {{ c.name }}
                  </v-list-item-title>
                </v-list-item-content>
              </v-list-item>
            </v-list>
          </div>
        </v-col>
        <v-col md="9">
          <v-row>
            <template>
              <v-col
                cols="12"
                md="6"
                v-for="(p, i) in filteredProducts"
                :key="`product${i}-${i}`"
              >
                <v-card
                  nuxt
                  :to="`/products/${p.id}`"
                  color="surface"
                  class="el ma-2 mb-5 mr-5"
                >
                  <v-img :src="p.image" height="300">
                    <template #placeholder>
                      <v-row
                        class="fill-height"
                        justify="center"
                        align="center"
                      >
                        <v-progress-circular
                          width="2"
                          size="100"
                          color="primary"
                          indeterminate
                        >
                        </v-progress-circular>
                      </v-row>
                    </template>
                  </v-img>
                  <v-card-title class="text-md-body-1 font-weight-bold">
                    {{ p.name }}
                  </v-card-title>
                  <v-card-subtitle class="primary--text pb-3">
                    {{ $formatMoney(p.price) }}
                  </v-card-subtitle>
                  <v-card-text>
                    <v-chip
                      x-small
                      label
                      outlined
                      class="mr-1"
                      v-for="(t, i) in p.tags"
                      :key="`prod${p.id}-${i}`"
                    >
                      {{ t }}
                    </v-chip>
                  </v-card-text>
                </v-card>
              </v-col>
            </template>
          </v-row>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  async created() {
    this.categories = await this.$content('category').fetch()
    this.products = await this.$content('products').fetch()
  },
  data() {
    return {
      products: null,
      categories: null,
      search: null,
      selectedCategory: null, 
    }
  },
  computed: {
    filteredProducts() {
      if (!this.products) return [];

      const searchLower = this.search ? this.search.toLowerCase() : '';
      const categoryFilter = this.selectedCategory
        ? this.selectedCategory.toLowerCase()
        : '';

      return this.products.filter((p) => {
        const nameLower = p.name.toLowerCase();
        const price = p.price.toString();
        const salePrice = p.selPrice?.toString() || '';
        const rating = p.ratings.toString();

  
        const categoryMatch =
          !categoryFilter || p.tags.some((tag) => tag.toLowerCase().includes(categoryFilter));

        const searchMatch =
          !searchLower ||
          nameLower.includes(searchLower) ||
          price.includes(searchLower) ||
          salePrice.includes(searchLower) ||
          rating.includes(searchLower);

        return categoryMatch && searchMatch;
      });
    },
  },
  methods: {
    selectCategory(categoryName) {

      this.selectedCategory = categoryName;
    },
  },
}
</script>

<style></style>
