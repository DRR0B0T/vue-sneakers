<script setup>
import Card from './Card.vue'

const onFavoriteAdd = () => {
  alert('Favorite Added')
}
const onClickAdd = () => {
  alert('item Added')
}
</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
      :isAdded="false"
      :isFavorite="false"
      :onClickAdd="onClickAdd"
      :onFavoriteAdd="onFavoriteAdd"
      :price="3500"
      imageUrl="/sneakers/sneakers-1.jpg"
      title="Мужские кроссовки Nike Blazer Mid Suede"
    />
  </div>
</template>

<style scoped></style>
