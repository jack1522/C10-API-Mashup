<script setup>
import WelcomeItem from "./WelcomeItem.vue";
import DocumentationIcon from "./icons/IconDocumentation.vue";
import ToolingIcon from "./icons/IconTooling.vue";
import EcosystemIcon from "./icons/IconEcosystem.vue";
import CommunityIcon from "./icons/IconCommunity.vue";
import SupportIcon from "./icons/IconSupport.vue";
import { ref, onMounted } from "vue";

import axios from "axios";

const recipes = ref([]);

onMounted(async () => {
  const recipeResp = await axios.get("https://dummyjson.com/recipes");
  recipes.value = recipeResp.data.recipes.slice(0, 3);
});
</script>

<template>
  <h1 class="title">TOP RECIPES</h1>
  <div v-for="(recipe, id) in recipes" :key="id">
    <h2 class="name">&starf;{{ recipe.name }}</h2>

    <h3 class="ing">
      Ingredients :
      <span v-for="(ingredients, id) in recipe.ingredients" :key="id">
        {{ ingredients }},
      </span>
    </h3>
    <h3 class="ing">Instructions :</h3>

    <ol>
      <li v-for="(instructions, id) in recipe.instructions" :key="id">
        {{ instructions }}
      </li>
    </ol>
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
</style>
