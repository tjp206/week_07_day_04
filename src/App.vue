<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import { eventBus } from './main.js'
import BeerDetail from './components/BeerDetail.vue'
import BeerList from './components/BeerList.vue'

export default {
  name: 'App',
  data() {
    return {
      beers: [],
      seelectedBeer: null,
    };
  },
  mounted() {
    fetch('https://api.punkapi.com/v2/beers')
    .then(res = res.json())
    .then(beers => this.beers = data)

    eventBus.$on('beer-selected', (beer) => {
      this.selectedBeer = beer
    })
  },
  components: {
    
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
