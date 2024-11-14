<script setup>
import Card from './Card.vue'

defineProps({
  items: Array,
  isFavorites: Boolean,
})
const emit = defineEmits(['onFavoriteAdd', 'onAddToCart'])
</script>

<template>
  <div v-auto-animate class="grid grid-cols-4 gap-5 mt-5">
    <Card
      v-for="item in items"
      :id="item.id"
      :key="item.id"
      :if-favorites="isFavorites"
      :imageUrl="item.imageUrl"
      :isAdded="item.isAdded"
      :isFavorite="item.isFavorite"
      :onAddToCart="isFavorites ? null : () => emit('onAddToCart', item)"
      :onClickFavorite="isFavorites ? null : () => emit('onFavoriteAdd', item)"
      :price="item.price"
      :title="item.title"
    />
  </div>
</template>

<style scoped></style>
