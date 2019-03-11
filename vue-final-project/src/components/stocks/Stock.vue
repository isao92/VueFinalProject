<template>
  <div>
    <h4>This is the stocks - Stock</h4>
    <div>
      <h2>{{ stock.name }}</h2>
      <h5>(Price: {{ stock.price }})</h5>
    </div>
    <div>
      <input type="number" placeholder="Quantity" v-model="quantity">
    </div>
    <div>
      <button @click="buyStock" :disabled="quantity <= 0">Buy</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['stock'],
  data () {
    return {
      quantity: 0
    }
  },
  methods: {
    buyStock () {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity
      }
      console.log(order)
      this.quanity = 0
    }
  }
}
</script>
