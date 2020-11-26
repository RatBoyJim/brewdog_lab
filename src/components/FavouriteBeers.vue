<template>
  <div class="beer-list">
    <h2>Favourite Beers:</h2>
    <h3 v-for="(beer, index) in favouriteBeers" :key="index">
      {{ beer.name }}
      <button v-on:click="removeFromFavourites(index)">
        Remove Beer from favourites list
      </button>
    </h3>
  </div>
</template>

<script>
export default {
  name: "favourite-beers",
  props: ["favouriteBeers"],
  methods: {
    removeFromFavourites(index) {
      this.favouriteBeers.splice(index, 1);
    },
  },
};
</script>

<style>
.beer-list {
  border: solid 2px burlywood;
}
</style>
