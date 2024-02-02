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

    <div>
      <div class="filter">
        <p>Filtrer par tag :</p>
        <button
            v-for="tag in tags?.data"
            :key="tag.id"
            :class="['tag-button', { 'active': search.queryTags.includes(tag.slug) }]"
            :title="tag.name"
            @click="addTag(tag.slug)"
        >
          {{ tag.name }}
        </button>

      </div>

    </div>

  </div>

  <hr class="solid">

  <div class="card_container" v-if="search.sortedByTags.length">
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
  flex-direction: column;
  align-items: center;
}

.filter{
  display: flex;
  flex-direction: row;
  gap: 15px;
  align-items: center;
}

.card_container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  padding: 20px;
  gap: 30px;

}

hr.solid {
  border-top: 3px solid #951E1A;
}

.tag-button {
  padding: 0.5rem 1rem;
  border: none;
  cursor: pointer;
}

.tag-button.active {
  background-color: #954d25;
  color: #fff;
}

.tag-button:not(.active) {
  background-color: #9e7c60;
  color: #333;
}
</style>