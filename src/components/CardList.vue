<script setup>
import Card from './Card.vue'

defineProps({
  items: Array,
})

const onFavoriteAdd = () => {
  alert('Favorite Added')
}
const onClickAdd = () => {
  alert('item Added')
}
</script>

<template>
  <div class="grid grid-cols-4 gap-5 mt-5">
    <Card
      v-for="item in items"
      :key="item.id"
      :imageUrl="item.imageUrl"
      :isAdded="false"
      :isFavorite="item.isFavorite"
      :onClickAdd="onClickAdd"
      :onFavoriteAdd="onFavoriteAdd"
      :price="item.price"
      :title="item.title"
    />
  </div>
</template>

<style scoped></style>
