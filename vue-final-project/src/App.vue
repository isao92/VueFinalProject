<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Stock Trader</router-link> |
      <router-link to="/about">About</router-link> |
      <router-link to="/portfolio">Portfolio</router-link> |
      <router-link to="/stocks">Stocks</router-link> |
      <strong>Funds: {{ funds | currency }}</strong> |
      <a href="#" @click="endDay">End Day</a>
    </div>
    <transition name="slide" mode="out-in">
    <router-view/>
    </transition>
  </div>
</template>

<script>
import { mapActions } from 'vuex'
export default {
  created () {
    this.$store.dispatch('initStocks')
  },
  computed: {
    funds () {
      return this.$store.getters.funds
    }
  },
  methods: {
    ...mapActions([
      'randomizeStocks'
    ]),
    endDay () {
      this.randomizeStocks()
    }
  }
}
</script>

<style>
.slide-enter-active {
  animation: slide-in 200ms ease-out forwards;
}

.slide-leave-active {
  animation: slide-out 200ms ease-out forwards;
}

@keyframes slide-in {
  from {
    transform: translateY(-30px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}
@keyframes slide-out {
  from {
    transform: translateY(0);
    opacity: 1;
  }
  to {
    transform: translateY(-30px);
    opacity: 0;
  }
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
