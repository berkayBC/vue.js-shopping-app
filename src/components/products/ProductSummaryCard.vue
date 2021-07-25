<template>
  <div class="card">
    <img class="img" :src="product.img" />
    <h3>{{ product.Title }}</h3>
    <h3>{{ product.price }}$</h3>

    <button class="view-product-button" @click="$emit(`view-product`, product)">
      Product Details
    </button>
    <div class="button-container">
      <button class="remove" @click="removeFromCart">Remove from Cart</button>
      <button class="add" @click="addToCart">Add to Cart</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["product"],
  computed: {
    description() {
      return this.product.Description;
    },
  },
  methods: {
    addToCart() {
      this.$store.commit("addToCart", this.product);
    },
    removeFromCart() {
      this.$store.commit("removeFromCart", this.product);
    },
  },
};
</script>

<style lang="scss" scoped>
.card {
  width: 80%;
  margin: 1%;
  padding: 5px;
  border-radius: 3px;
  background-color: whitesmoke;
  box-shadow: 0 0 5px gray;
}

.img {
  border: 2px solid red;
  border-radius: 8px;
  width: 250px;
}
button.view-product-button {
  padding: 10px;
  background-color: rgb(79, 160, 187);
  border: none;
  color: white;
  font-weight: bold;
  font-size: 1rem;
  border-radius: 2px;
  cursor: pointer;
}
@media (min-width: 500px) {
  .card {
    width: 350px;
    margin: 10px;
  }
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
</style>