<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";

const recipes = ref([]);

onMounted(async () => {
  const recipeResp = await axios.get("https://dummyjson.com/recipes");
  recipes.value = recipeResp.data.recipes.slice(0, 10);
});
</script>

<template>
  <h1 class="title">ALL DAY DINING MENU</h1>
  <div v-for="(recipe, id) in recipes" :key="id">
    <img :src="recipe.image" alt="foodImg" class="foodImg" />
    <h2 class="name">
      {{ recipe.name }} |
      <span class="fakeprice">${{ recipe.cookTimeMinutes }}</span>
    </h2>

    <h3 class="ing">
      Served with :
      <span v-for="(ingredients, id) in recipe.ingredients" :key="id">
        {{ ingredients }},
      </span>
    </h3>

    <p>
      CALORIES : {{ recipe.caloriesPerServing }} | RATING
      {{ recipe.rating }} &starf; ( {{ recipe.reviewCount }} reviews)
    </p>

    <hr />
  </div>
</template>

<style scoped>
.name {
  color: #ff9885;
}
.title {
  color: #42b883;
  text-decoration: underline dashed;
}

.ing {
  font-style: italic;
  color: #35495e;
}

.foodImg {
  width: 25%;
  padding-top: 10px;
}

.fakeprice {
  font-style: italic;
  color: #35495e;
}
</style>
