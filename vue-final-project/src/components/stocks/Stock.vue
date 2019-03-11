<template>
  <div>
    <h4>This is the stocks - Stock</h4>
    <div>
      <h2>{{ stock.name }}</h2>
      <h5>(Price: {{ stock.price }})</h5>
    </div>
    <div>
      <input type="number" placeholder="Quantity" v-model="quantity" :class="{danger: insufficientFunds}">
    </div>
    <div>
      <button @click="buyStock" :disabled="insufficientFunds || quantity <= 0">{{ insufficientFunds ? 'insufficient Funds' : 'Buy'}}</button>
    </div>
  </div>
</template>

<style scoped>
  .danger{
    border: 2px solid red
  }
</style>

<script>
export default {
  props: ['stock'],
  data () {
    return {
      quantity: 0
    }
  },
  computed: {
    funds () {
      return this.$store.getters.funds
    },
    insufficientFunds () {
      return this.quantity * this.stock.price > this.funds
    }
  },
  methods: {
    buyStock () {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity
      }
      this.$store.dispatch('buyStock', order)
      this.quanity = 0
    }
  }
}
</script>
