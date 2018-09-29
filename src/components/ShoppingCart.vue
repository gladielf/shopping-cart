<template>
  <div>
    <h1>Shopping Cart</h1>
    <ul>
      <li v-for="product in products" :key="product.id">
        {{product.title}} - {{product.price | currency}} - {{product.quantity}}
      </li>
    </ul>
    <p>Total: {{total | currency}} </p>
    <button @click="checkout" :disabled="btndisabled" >Checkout</button>
    <p v-if="checkoutStatus"> {{checkoutStatus}} </p>
  </div>
</template>

<script>
  import { mapState, mapGetters, mapActions } from 'vuex'
  export default {
    name: 'shopping-cart',
    computed: {
      ...mapState('cart', {
            checkoutStatus : state => state.checkoutStatus,
            btndisabled : state => state.items.length === 0
      }),
      ...mapGetters('cart', {
            products: 'cartProducts',
            total: 'cartTotal'
      })
    },
    methods: {
        ...mapActions('cart', ['checkout'])
    }
  }
</script>

<style scoped>

</style>