<script setup>
defineProps({
  imageUrl: String,
  title: String,
  price: Number,
  isFavorite: Boolean,
  isAdded: Boolean,
  onClickAdd: Function,
  onFavoriteAdd: Function,
})
</script>

<template>
  <div
    class="flex flex-col justify-between bg-white relative border border-slate-100 rounded-3xl p-8 cursor-pointer transition hover:-translate-y-2 hover:shadow-xl"
  >
    <img
      :src="!isFavorite ? '/like-1.svg' : '/like-2.svg'"
      alt="Like 2"
      class="absolute top-8 left-8"
      @click="onFavoriteAdd"
    />

    <img :src="imageUrl" alt="Sneakers" />

    <p class="mt-2">{{ title }}</p>

    <div class="flex justify-between mt-2">
      <div class="flex flex-col">
        <span class="text-slate-400">Цена:</span>
        <b>{{ price }} руб.</b>
      </div>
      <img
        :src="!isAdded ? ' /plus.svg' : '/checked.svg'"
        alt="Plus"
        @click="onClickAdd"
      />
    </div>
  </div>
</template>

<style scoped></style>
