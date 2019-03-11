<template>
  <div>
    <h4>This is the portfolio/Stock.vue</h4>
    <div>
      <h2>{{ stock.name }}</h2>
      <h5>(Price: {{ stock.price }} | Quantity: {{ stock.quantity }})</h5>
    </div>
    <div>
      <input type="number" placeholder="Quantity" v-model="quantity">
    </div>
    <div>
      <button @click="sellStock" :disabled="insufficientQuantity || quantity <= 0">{{ insufficientQuantity ? 'Not enough Stocks' : 'Sell' }}</button>
    </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex'
export default {
  props: ['stock'],
  data () {
    return {
      quantity: 0
    }
  },
  computed: {
    insufficientQuantity () {
      return this.quantity > this.stock.quantity
    }
  },
  methods: {
    ...mapActions({
      placeSellOrder: 'sellStock'
    }),
    sellStock () {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity
      }
      this.placeSellOrder(order)
      this.quantity = 0
    }
  }
}
</script>
