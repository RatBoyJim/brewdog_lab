<template>
  <div>
    <view-all-beers :beers="this.beers"></view-all-beers>
    <beer-details :selectedBeer="this.selectedBeer"></beer-details>
    <favourite-beers :favouriteBeers="this.favouriteBeers"></favourite-beers>
    <button v-on:click="addToFavourites">Add Beer to favourites</button>
  </div>
</template>

<script>
import FavouriteBeers from "./components/FavouriteBeers.vue";
import ViewAllBeers from "./components/ViewAllBeers.vue";
import ViewBeerDetails from "./components/ViewBeerDetails.vue";

import { eventBus } from "./main.js";
export default {
  name: "app",
  data() {
    return {
      beers: [],
      selectedBeer: null,
      favouriteBeers: [],
    };
  },
  methods: {
    addToFavourites(selectedBeer) {
      if (this.favouriteBeers.includes(this.selectedBeer)) {
        return;
      } else {
        this.favouriteBeers.push(this.selectedBeer);
      }
    },
    fetchData: async function getPages() {
      // set some variables
      const baseUrl = `https://api.punkapi.com/v2/beers?page=`;
      let page = 1;
      // create a lastResult array which is going to be used to check if there is a next page
      let lastResult = [];
      do {
        // try catch to catch any errors in the async api call
        try {
          // use node-fetch to make api call
          const resp = await fetch(`${baseUrl}${page}`)
            .then((response) => response.json())
            .then((data) => (this.beers = [...this.beers, ...data]));
          page++;
        } catch (err) {
          console.error(`Oops, something is wrong ${err}`);
        }
        // keep running until there's no next page
      } while (lastResult.next !== null);
    },
  },
  mounted() {
    this.fetchData();
    eventBus.$on("beer-selected", (beer) => {
      this.selectedBeer = beer;
    });
  },
  components: {
    "view-all-beers": ViewAllBeers,
    "beer-details": ViewBeerDetails,
    "favourite-beers": FavouriteBeers,
  },
};
</script>

<style>
body {
  font-family: Arial;
}
</style>
