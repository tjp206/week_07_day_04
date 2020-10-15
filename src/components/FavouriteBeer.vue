<template lang="html">
  <div id="favs">
      <h3>Favourite Beers</h3>
      <ul>
          <li v-for="favouriteBeer in favouriteBeers">{{ favouriteBeer.name }}: {{ favouriteBeer.tagline }} <img class="fav-beer-img" :src="favouriteBeer.image_url" /></li>
      </ul>
  </div>
</template>

<script>
export default {
    name: 'favourite-beers',
    props: ['favouriteBeers']
}
</script>

<style>
</style>