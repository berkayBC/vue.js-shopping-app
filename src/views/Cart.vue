<template>
    <div>
        <h1> Your Cart </h1>

        <CartItemCard
        v-for="product in products"
        :key="product.Title" 
        :product="product"
        />
        
        <CartSummary
        />
    </div>
</template>

<script>
import CartItemCard from "../components/CartItemCard.vue"
import CartSummary from "../components/CartSummary.vue"

export default {
    components: {
        CartItemCard,
        CartSummary
    },
    
    computed: {
        products() {
            return this.$store.getters.cartItems
        }
    }
}
</script>