<template>
  <v-col cols="12" sm="4">
    <v-card>
      <v-img
        :src="product.image"
        class="white--text align-end"
        gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
        height="400px"
      >
        <ProductCard
          :product="product"
          :addToCart="addToCart"
          :removeFromCart="removeFromCart"
          :addToFavorites="addToFavorites"
          :removeFromFavorites="removeFromFavorites"
          :isInFavorites="this.checkIfProductInFavorites"
          :isInCart="this.checkIfProductInCart"
        />
      </v-img>

      <v-card-actions>
        <div>${{ product.price }}</div>
        <v-spacer></v-spacer>

        <v-btn
          icon
          v-if="this.checkIfProductInFavorites"
          v-on:click="removeFromFavorites(product)"
        >
          <v-icon>mdi-heart</v-icon>
        </v-btn>
        <v-btn icon v-else v-on:click="addToFavorites(product)">
          <v-icon>mdi-heart-outline</v-icon>
        </v-btn>

        <v-btn
          icon
          v-if="this.checkIfProductInCart"
          v-on:click="removeFromCart(product)"
        >
          <v-icon>mdi-cart</v-icon>
        </v-btn>
        <v-btn icon v-else v-on:click="addToCart(product)">
          <v-icon>mdi-cart-outline</v-icon>
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-col>
</template>

<script>
import { mapGetters, mapActions } from "vuex";
import ProductCard from "./ProductCard";

export default {
  name: "Product",
  props: ["product"],
  components: {
    ProductCard,
  },
  data: () => ({
    dialog: false,
  }),
  methods: {
    ...mapActions([
      "addToCart",
      "removeFromCart",
      "addToFavorites",
      "removeFromFavorites",
    ]),
  },
  computed: {
    ...mapGetters(["isProductInCart", "isProductInFavorites"]),
    checkIfProductInCart() {
      return this.isProductInCart(this.product.id);
    },
    checkIfProductInFavorites() {
      return this.isProductInFavorites(this.product.id);
    },
  },
};
</script>
