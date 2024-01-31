<script lang="ts" setup>
import Card from "~/components/Card.vue";
import type {ITag} from '~/models/search.model'

const { find } = useStrapi()
const search = useSearchStore()

const { data: tags } = useAsyncData(
    'tags',
    () => find<{ data: ITag[] }>('tags'),
)

function addTag(tag: string) {
  if (!search.queryTags.includes(tag))
    search.queryTags.push(tag)
  else search.queryTags = search.queryTags.filter(t => t !== tag)
}


</script>

<template>

  <div class="header">
    <h1>Mon Blog de recettes </h1>
    <div class="search">
      <label for="search">Chercher une recette :</label>
      <input id="search" v-model="search.query" class="px-4 py-2" type="search">
    </div>

  </div>
  <hr class="solid">



  <div v-if="search.sortedByTags.length">
    <Card
        v-for="recipe in search.sortedByTags"
        :key="recipe.id"
        :recipe="recipe"
    />
  </div>
  <p v-else>
    Aucun résultat pour cette recherche
  </p>


</template>


<style scoped>

.header{
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
}

.search{
  display: flex;
  flex-direction: row;
  gap: 15px;
  align-items: center;
}

hr.solid {
  border-top: 3px solid #951E1A;
}


</style>