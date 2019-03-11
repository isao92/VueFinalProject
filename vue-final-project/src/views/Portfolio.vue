<template>
  <div>
    <div>
      <app-stock v-for="(stock, index) in stocks" :key="index.id" :stock="stock"></app-stock>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import Stock from '../components/portfolio/Stock.vue'
export default {
  computed: {
    ...mapGetters({
      stocks: 'stockPortfolio'
    })
  },
  components: {
    appStock: Stock
  }
}
</script>
