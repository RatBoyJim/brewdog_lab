<template>
  <div v-if="selectedBeer" id="selected-beer">
    <h2>{{ selectedBeer.name }}</h2>
    <img
      id="smaller-beer"
      :src="selectedBeer.image_url"
      alt="selectedBeer image"
    />
    <p>ABV: {{ selectedBeer.abv }}%</p>
    <view-beer-ingredients :selectedBeer="selectedBeer"></view-beer-ingredients>
  </div>
</template>

<script>
import ViewBeerIngredients from "./ViewBeerIngredients";
export default {
  name: "beer-detail",
  props: ["selectedBeer"],
  components: {
    "view-beer-ingredients": ViewBeerIngredients,
  },
};
</script>

<style>
#smaller-beer {
  height: 200px;
}
</style>
