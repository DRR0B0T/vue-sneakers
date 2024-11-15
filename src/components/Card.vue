<script setup>
defineProps({
  id: Number,
  imageUrl: String,
  title: String,
  price: Number,
  year: Number,
  isFavorite: Boolean,
  isAdded: Boolean,
  onAddToCart: Function,
  onClickFavorite: Function,
})
</script>

<template>
  <div
    class="flex flex-col justify-between bg-white relative border border-slate-100 rounded-3xl p-8 cursor-pointer transition hover:-translate-y-2 hover:shadow-xl"
  >
    <img
      v-if="onClickFavorite"
      :src="!isFavorite ? '/like-1.svg' : '/like-2.svg'"
      alt="Like 2"
      class="absolute top-8 left-8"
      @click="onClickFavorite"
    />

    <img :src="imageUrl" alt="Sneakers" class="h-52" />

    <p class="mt-2">{{ title }}</p>

    <div class="flex justify-between mt-2">
      <div class="flex flex-col">
        <span class="text-slate-400">Цена:</span>
        <b>{{ price }} ₽</b>
      </div>
      <img
        v-if="onAddToCart"
        :src="!isAdded ? ' /plus.svg' : '/checked.svg'"
        alt="Plus"
        @click="onAddToCart"
      />
    </div>
  </div>
</template>

<style scoped></style>
