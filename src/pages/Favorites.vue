<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'

const favorites = ref([])

onMounted(async () => {
  try {
    const { data } = await axios.get(
      `https://fd192f320b005090.mokky.dev/favorites`,
    )
  } catch (e) {
    console.error(e)
  }
})
</script>

<template>
  <h1>Favorites</h1>
</template>

<style scoped></style>
