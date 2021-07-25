<template>
  <h1>Kalite-Shop</h1>
  <input type="text" v-model="search" placeholder="Search Product" />
  <div class="home">
    <ProductDescriptionDrawer
      :product="product"
      :active="active.product_drawer"
      v-on:close-product-drawer="closeProductDrawer()"
    />

    <div class="product-cards-container">
      <ProductSummaryCard
        v-for="product in filteredProducts"
        :key="product.Title"
        :product="product"
        v-on:view-product="viewProduct($event)"
      />
    </div>
  </div>
</template>

<script>
import ProductSummaryCard from "../components/products/ProductSummaryCard.vue";
import ProductDescriptionDrawer from "../components/products/ProductDescriptionDrawer.vue";
import json from "../components/products/products.json";

export default {
  name: "Home",
  components: {
    ProductSummaryCard,
    ProductDescriptionDrawer,
  },
  data() {
    return {
      items: json.items,
      product: null,
      active: {
        product_drawer: false,
      },
      search: "",
    };
  },
  mounted() {
    this.setPrice();
    // console.log(this.items) // test
  },
  methods: {
    setPrice() {
      for (let i = 10, j = 0; j < this.items.length; i += 10, j++) {
        this.items[j]["price"] = i;
      }
    },
    viewProduct(product) {
      this.product = product;
      this.active.product_drawer = true;
      // console.log(this.product); // test
    },
    closeProductDrawer() {
      this.active.product_drawer = false;
    },
  },
  computed: {
    filteredProducts: function () {
      return this.items.filter((product) => {
        return product.Title.toLowerCase().match(this.search.toLowerCase());
      });
    },
  },
};
</script>

<style lang="scss">
.product-cards-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
</style>
