<script setup>
import Card from './Card.vue'

defineProps({
  items: Array,
})
const emit = defineEmits(['onFavoriteAdd'])

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
      :isAdded="false"
      :isFavorite="item.isFavorite"
      :onClickAdd="onClickAdd"
      :onClickFavorite="() => emit('onFavoriteAdd', item)"
      :price="item.price"
      :title="item.title"
    />
  </div>
</template>

<style scoped></style>
