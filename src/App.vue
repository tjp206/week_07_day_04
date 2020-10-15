<template>
  <div id="app">
    <h1>Welcome to BrewDog</h1>
    <section>
      <label for="character-selected">Select a beer:</label>
      <select id="character-selected" v-model="selectedBeer">
        <option disabled value="">Choose your beer</option>
        <option v-for="(beer, index) in beers" :value="beer" :key='index'>{{beer.name}}</option>
      </select>
      <!-- <beer-list :beers="beers"></beer-list> -->
      <beer-detail :beer="selectedBeer"></beer-detail><br><br>

      <button class="fav-button" v-if="!favouriteBeers.includes(selectedBeer)" v-on:click="addToFav">Add as favourite</button>

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
    let urls = [
    "https://api.punkapi.com/v2/beers?page=1&per_page=80",
    "https://api.punkapi.com/v2/beers?page=2&per_page=80",
    "https://api.punkapi.com/v2/beers?page=3&per_page=80",
    "https://api.punkapi.com/v2/beers?page=4&per_page=80",
    "https://api.punkapi.com/v2/beers?page=5&per_page=80",
  ]
  let requests = urls.map(url => fetch(url));
  Promise.all(requests)
  .then(responses => Promise.all(responses.map(res => res.json())))
  .then(data => data = [].concat.apply([], data))
  .then(mergedData => this.beers = mergedData),

    this.getBeers(),
    eventBus.$on('deleted-beer', (beer) => {
        this.deleteFromFav(beer);
    })
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
    deleteFromFav: function(favouriteBeer) {
      let index = this.favouriteBeers.indexOf(favouriteBeer);
      console.log(favouriteBeer);
      this.favouriteBeers.splice(index, 1);
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

.x{
  color: red;
  background-color: black;
  border-radius: 25%;
  border: 2px solid red;
  font-size: 9px;
}

.x:hover {
  background-color: red;
  color: black;
}

.fav-button{
  font-size: 20px;
  color:white;
  background-color: black;
  border: 2px solid whitesmoke;
}

.fav-button:hover {
  background-color:whitesmoke;
  color: black;
  box-shadow: 0 0 5px 5px slategrey;
}

button {
transition-duration: 0.5s;
}
</style>
