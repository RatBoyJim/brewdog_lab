<template>
  <div class="beer-select">
    <label for="beer-select">Select A Beer:</label>
    <select
      name="beer-select"
      id="beer-select"
      @change="onChange"
      v-model="selectedBeer"
    >
      <option disabled value="">Select a beer...</option>
      <option v-for="beer in beers" :key="beer.id" :value="beer">{{
        beer.name
      }}</option>
    </select>
  </div>
</template>

<script>
import { eventBus } from "../main.js";
export default {
  name: "view-all-beers",
  data() {
    return {
      selectedBeer: null,
    };
  },
  props: ["beers"],
  methods: {
    onChange() {
      eventBus.$emit("beer-selected", this.selectedBeer);
    },
  },
};
</script>

<style></style>
