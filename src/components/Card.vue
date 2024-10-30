<script setup>
import { inject } from 'vue'

const props = defineProps({
  id: Number,
  imageUrl: String,
  title: String,
  price: Number,
  year: Number,
  isFavorite: Boolean,
  isAdded: Boolean,
  onClickAdd: Function,
})

const onFavoriteAdd = inject('onFavoriteAdd')

const onClickFavorite = () => {
  const obj = {
    ...props,
    parentId: props.id,
  }
  onFavoriteAdd(obj)
}
</script>

<template>
  <div
    class="flex flex-col justify-between bg-white relative border border-slate-100 rounded-3xl p-8 cursor-pointer transition hover:-translate-y-2 hover:shadow-xl"
  >
    <img
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
        :src="!isAdded ? ' /plus.svg' : '/checked.svg'"
        alt="Plus"
        @click="onClickAdd"
      />
    </div>
  </div>
</template>

<style scoped></style>
