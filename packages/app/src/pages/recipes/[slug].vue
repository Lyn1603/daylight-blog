<script lang="ts" setup>

const { findOne } = useStrapi4()
const route = useRoute()

const { data: recipe, pending, error } = useAsyncData('recipe',
    () => findOne(`recipes/${route.params.slug}`)
)

onMounted(() => {
  console.log({recipe, pending, error })
})

</script>

<template>
  <div class="container">
    <NuxtLink :to="`/`"> Retour </NuxtLink>
    <div v-if="pending"> Chargement...</div>
    <div v-if="recipe">

      <h2 >{{ recipe.data.title }}</h2>
      <img :src=recipe.data.image.url alt="images">
      <p> {{ recipe.data.description}}</p>

    </div>
  </div>
</template>


<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: #bca38d;
  color: #fff;
}

h2 {
  font-size: 1.8rem;
  margin-bottom: 10px;
}

p {
  font-size: 1.2rem;
  line-height: 1.6;
}

img {
  max-width: 100%;
  height: auto;
  margin-bottom: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

a {
  display: inline-block;
  background-color: #9e7c60;
  color: #fff;
  padding: 10px 20px;
  border-radius: 5px;
  text-decoration: none;
  transition: background-color 0.3s ease;
}

a:hover {
  background-color: #954d25;
}

.template {
  display: block;
  text-align: center;
  margin-top: 20px;
  font-size: 1.4rem;
}


</style>