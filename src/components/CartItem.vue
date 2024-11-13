<script setup>
const emit = defineEmits(['onClickRemove'])

defineProps({
  id: Number,
  imageUrl: String,
  title: String,
  price: Number,
})
</script>

<template>
  <div class="flex items-center gap-4 border border-slate-100 p-4 rounded-xl">
    <img :src="imageUrl" alt="Sneakers" class="w-16 h-16" />

    <div class="flex flex-col justify-between">
      <p>{{ title }}</p>
      <div class="flex justify-between mt-2">
        <b>{{ price }} ₽</b>
        <img
          alt="Close card"
          class="opacity-40 hover:opacity-100 transition cursor-pointer"
          src="/close.svg"
          @click="() => emit('onClickRemove')"
        />
      </div>
    </div>
  </div>
</template>
