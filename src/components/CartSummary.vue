<template>
    <div class="cart-item-card">
        <h3>Cart Total: {{cart_total}}$</h3>

        <button class="view-product-button">BUY!</button>
    </div>
</template>

<script>
export default {

    computed: {
        cart_total() {
            return this.$store.getters.cartTotal
        }
    }
}
</script>

<style lang="scss">
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
</style>