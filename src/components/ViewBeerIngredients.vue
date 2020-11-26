<template>
  <div>
    <p v-for="(ingredient, index) in ingredientsList" :key="index">
      {{ ingredient }}
    </p>
  </div>
</template>

<script>
export default {
  name: "view-beer-ingredients",
  props: ["selectedBeer"],
  computed: {
    ingredientsList(selectedBeer) {
      let ingredients = [];

      console.log("selectedBeer", this.selectedBeer);
      console.log("selectedBeer.ingredients", this.selectedBeer.ingredients);
      console.log("hops", this.selectedBeer.ingredients.hops[0].name);
      console.log("malt", this.selectedBeer.ingredients.malt[0].name);

      for (let i = 0; i < this.selectedBeer.ingredients.malt.length; i++) {
        const malt = this.selectedBeer.ingredients.malt[i];
        ingredients.push(malt.name);
      }
      for (let i = 0; i < this.selectedBeer.ingredients.malt.length; i++) {
        const hop = this.selectedBeer.ingredients.hops[i];
        ingredients.push(hop.name);
      }
      let uniqueIngredients = [...new Set(ingredients)];
      console.log(ingredients);
      console.log(uniqueIngredients);
      return uniqueIngredients;
    },
  },
  mounted() {},
};
</script>

<style></style>
