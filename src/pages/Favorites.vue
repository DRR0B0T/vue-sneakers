<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'
import CardList from '@/components/CardList.vue'

const favorites = ref([])

onMounted(async () => {
  try {
    const { data } = await axios.get(
      `https://fd192f320b005090.mokky.dev/favorites?_relations=items`,
    )

    favorites.value = data.map(obj => obj.item)
  } catch (e) {
    console.error(e)
  }
})
</script>

<template>
  <h2 class="text-4xl font-bold">Мои закладки</h2>
  <CardList :is-favorites="true" :items="favorites" />
</template>

<style scoped></style>
