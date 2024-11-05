<script setup>
defineProps({
  imageUrl: String,
  title: String,
  description: String,
})
</script>

<template>
  <div class="flex-col flex text-center items-center mx-auto w-72">
    <img :src="imageUrl" alt="Info picture" height="80" width="80" />
    <h2 class="mt-4 text-2xl font-medium">{{ title }}</h2>
    <p class="text-gray-400 mt-1">{{ description }}</p>
  </div>
</template>
