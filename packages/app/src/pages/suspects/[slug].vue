<script lang="ts" setup>

const { findOne } = useStrapi4()
const route = useRoute()

const { data: suspect, pending, error } = useAsyncData('suspect',
    () => findOne(`suspects/${route.params.slug}`)
)

onMounted(() => {
  console.log({suspect, pending, error })
})

</script>

<template>
  <div class="container">
    <NuxtLink :to="`/`"> Retour </NuxtLink>
    <div v-if="pending"> Chargement...</div>
    <div v-if="suspect">

      <h2 >{{ suspect.data.title }}</h2>
      <img :src=suspect.data.idpicture.url alt="images">
      <p> {{ suspect.data.description}}</p>

    </div>
  </div>
</template>