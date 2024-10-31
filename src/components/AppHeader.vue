<script setup>
const emit = defineEmits(['openDrawer'])

defineProps({
  totalPrice: Number,
})
</script>

<template>
  <header
    class="bg-white flex items-center justify-between border-b border-slate-200 px-10 py-8"
  >
    <div class="flex items-center gap-4">
      <img alt="Logo" class="w-10" src="/logo.png" />
      <div>
        <h2 class="text-xl font-bold uppercase">Vue Sneakers</h2>
        <p class="text-slate-500">Магазин самых лучших кроссовок</p>
      </div>
    </div>
    <ul class="flex items-center gap-10">
      <li
        class="flex items-center gap-3 text-gray-500 hover:text-black cursor-pointer"
        @click="emit('openDrawer')"
      >
        <img alt="Cart" src="/cart.svg" />
        <b>{{ totalPrice }} руб.</b>
      </li>
      <li
        class="flex items-center gap-3 text-gray-500 hover:text-black cursor-pointer"
      >
        <img alt="Heart" src="/heart.svg" />
        <span>Закладки</span>
      </li>
      <li
        class="flex items-center gap-3 text-gray-500 hover:text-black cursor-pointer"
      >
        <img alt="Profile" src="/profile.svg" />
        <span>Профиль</span>
      </li>
    </ul>
  </header>
</template>

<style scoped></style>
