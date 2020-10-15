<template lang="html">
  <div id="favs">
      <h3>Favourite Beers</h3>
      <ul>
         <li v-for="favouriteBeer in favouriteBeers" :v-model="favourite">{{ favouriteBeer.name }}: {{ favouriteBeer.tagline }} <img class="fav-beer-img" :src="favouriteBeer.image_url"
         /> <button v-on:click="handleDelete(favouriteBeer)" class="x">X</button></li> 
      </ul>
  </div>
</template>

<script>
import { eventBus } from '../main.js'

export default {
    name: 'favourite-beers',
    props: ['favouriteBeers'],
    data() {
        return {
            favourite: null
        }
    },
    methods: {
        handleDelete(favourite) {
            eventBus.$emit('deleted-beer', favourite);
        },
    },
}
</script>

<style>
</style>