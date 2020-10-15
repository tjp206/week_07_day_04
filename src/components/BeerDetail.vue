<template>
  <div v-if="beer">
      <h2>{{ beer.name }}</h2>
      <p>{{ beer.tagline }}</p>
      <p>{{ beer.description }}</p>
      <p><img class="beer-img" :src="beer.image_url" /></p>
      

  </div>
</template>

<script>
export default {
    name:'beer-detail',
    props: ['beer']
}
</script>

<style>

</style>