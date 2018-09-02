<template>
  <div>
    <h1>Shopping Cart</h1>
    <ul>
      <li v-for="product in products" :key="product.id">
        {{product.title}} - {{product.price | currency}} - {{product.quantity}}
      </li>
    </ul>
    <p>Total: {{total | currency}} </p>
    <button @click="$store.dispatch('checkout')" :disabled="btndisabled" >Checkout</button>
    <p v-if="$store.state.checkoutStatus"> {{$store.state.checkoutStatus}} </p>
  </div>
</template>

<script>
  export default {
    name: 'shopping-cart',
    computed: {
      products () {
        return this.$store.getters.cartProducts
      },
      total () {
        return this.$store.getters.cartTotal
      },
      btndisabled () {
        return this.$store.state.cart.length === 0
      }
    }

  }
</script>

<style scoped>

</style>