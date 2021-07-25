<template>
  <div
    class="drawer-background"
    :class="{ show: active }"
    @click="$emit(`close-product-drawer`)"
  />

  <div class="drawer" :class="{ show: active }">
    <div class="drawer-close" @click="$emit(`close-product-drawer`)">x</div>

    <div v-if="product" class="product-details">
      <h2 class="text-center">{{ product.Title }}</h2>
      <img class="img" :src="product.img" />
      <h3 class="text-center">Price: {{ product.price }} $</h3>
      <h3 class="text-center">ID: {{ product.Id }}</h3>
      <h3 class="text-center">Maker: {{ product.Maker }}</h3>
      <p class="description">{{ product.Description }}</p>
      <h5 class="p-rating" v-if="product.Ratings">
        Ratings: {{ product.Ratings }}
      </h5>
      <h5 class="p-rating" v-else>Be the first one rating this item!</h5>

      <a class="p-link" :href="product.Url">For More Info</a>

      <div class="cart-total" v-if="product_total">
        <h3>In Cart: {{ product_total }}</h3>
      </div>

      <div class="button-container">
        <button class="remove" @click="removeFromCart">Remove from Cart</button>
        <button class="add" @click="addToCart">Add to Cart</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["product", "active"],
  emits: ["close-product-drawer"],
  methods: {
    addToCart() {
      this.$store.commit("addToCart", this.product);
    },
    removeFromCart() {
      this.$store.commit("removeFromCart", this.product);
    },
  },

  computed: {
    product_total() {
      return this.$store.getters.productQuantity(this.product);
    },
  },
};
</script> 

<style lang="scss">
.img {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}
.drawer-background {
  width: 100%;
  height: 100vh;
  position: fixed;
  left: 0;
  top: 0;
  background-color: rgba(124, 124, 124, 0.6);
  z-index: 100;
  display: none;
  transition: display 0.5s;

  &.show {
    display: block;
  }
}
.drawer {
  width: 95vw;
  height: 100vh;
  background-color: white;
  position: fixed;
  top: 0;
  left: -105vw;
  padding: 10px;
  transition: left 0.5s;
  z-index: 101;
  overflow-y: scroll;

  &.show {
    left: 0;
  }
}
.drawer-close {
  font-size: 1.5rem;
  padding: 4px;
  border-radius: 5px;
  right: 10px;
  border: 2px solid gray;
  color: gray;
  width: 15px;
  float: right;
  cursor: pointer;

  &:hover {
    background-color: lightgray;
  }
}
.product-details {
  display: flex;
  justify-content: center;
  flex-direction: column;

  p.description {
    padding: 10px;
    line-height: 1.5rem;
  }
  .button-container {
    button {
      width: 150px;
      border: none;
      padding: 10px;
      border-radius: 5px;
      margin: 0 5px 50px 5px;
      cursor: pointer;
    }
  }
}

@media (min-width: 500px) {
  .drawer {
    width: 450px;
  }
}
</style>