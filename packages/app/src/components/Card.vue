<script lang="ts" setup>

import type {IRecipe} from '~/models/search.model'

defineProps({
  recipe: {
    type: Object as PropType<IRecipe>,
    required: true,
  },
})

</script>


<template >


  <div class="card_container" >
    <div class="card">
      <h2>{{ recipe.title }}</h2>
      <img :src=recipe.image.url alt="images">
      <NuxtLink :to="`/recipes/${recipe.slug}`"> Voir les détails </NuxtLink>
    </div>
  </div>


</template>


<style scoped>

.card_container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;

}


.card {

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border-radius: 10px;
  border: solid #954d25 1px ;

}

.card h2 {
  font-size: 1.5rem;
  margin-bottom: 10px;
}

.card img {
  width: 50%;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  margin-bottom: 10px;
}


.card a {
  display: inline-block;
  background-color: #9e7c60;
  color: #fff;
  padding: 10px 20px;
  border-radius: 5px;
  text-decoration: none;
  transition: background-color 0.3s ease;
}

.card a:hover {
  background-color: #954d25;
}


</style>