<template>
  <div id="app">
    <h1>Welcome to BrewDog</h1>
    <section>
      <beer-list :beers="beers"></beer-list>
      <beer-detail :beer="selectedBeer"></beer-detail>

      <button v-if="!favouriteBeers.includes(selectedBeer)" v-on:click="addToFav">Add as favourite:</button>

      <favourite-beers :favouriteBeers="favouriteBeers"></favourite-beers>
      
    </section>
  </div>
</template>

<script>
import { eventBus } from './main.js'
import BeerDetail from './components/BeerDetail.vue'
import BeersList from './components/BeersList.vue'
import FavouriteBeer from  './components/FavouriteBeer.vue'

export default {
  name: 'App',
  data() {
    return {
      beers: [],
      selectedBeer: null,
      favouriteBeers: [],
    };
  },
  mounted() {
    this.getBeers()
  },
  components: {
    'beer-list': BeersList,
    'beer-detail': BeerDetail,
    'favourite-beers': FavouriteBeer
  },
  computed: {
    filterBeers: function() {
      return this.beers.fiter((beer) => {
        return this.selectedBeer.results.includes()
      })
    },
  },
  methods: {
    getBeers: function () {
      fetch('https://api.punkapi.com/v2/beers')
      .then(res => res.json())
      .then(data => this.beers = data)

      eventBus.$on('beer-selected', (beer) => {
        this.selectedBeer = beer
    })
    },
    addToFav: function() {
        this.favouriteBeers.push(this.selectedBeer)
      },
    deleteFromFav: function() {
        this.favouriteBeers.pop(this.selectedBeer)
    },
  }
}
</script>

<style>
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: black;
  color: whitesmoke;
  margin-top: 60px;
}

ul {
    list-style: none;
}

.beer-img {
  height: 250px;
}

.fav-beer-img {
  height: 50px;
}
</style>
