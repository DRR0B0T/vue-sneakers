<script setup>
import Card from './Card.vue'

defineProps({
  items: Array,
})
const emit = defineEmits(['onFavoriteAdd', 'onAddToCart'])

const onClickAdd = () => {
  alert('item Added')
}
</script>

<template>
  <div class="grid grid-cols-4 gap-5 mt-5">
    <Card
      v-for="item in items"
      :id="item.id"
      :key="item.id"
      :imageUrl="item.imageUrl"
      :isAdded="item.isAdded"
      :isFavorite="item.isFavorite"
      :onAddToCart="() => emit('onAddToCart', item)"
      :onClickAdd="onClickAdd"
      :onClickFavorite="() => emit('onFavoriteAdd', item)"
      :price="item.price"
      :title="item.title"
    />
  </div>
</template>

<style scoped></style>
