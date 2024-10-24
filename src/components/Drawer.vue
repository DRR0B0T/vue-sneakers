<script setup>
import DrawerHeader from '@/components/DrawerHeader.vue'
import CartListItem from '@/components/CartListItem.vue'
</script>

<template>
  <div class="fixed top-0 left-0 bg-black h-full w-full z-10 opacity-65"></div>
  <div class="bg-white h-full w-96 right-0 top-0 z-20 p-8 fixed">
    <DrawerHeader />
    <CartListItem />
    <div>
      <div class="flex gap-2">
        <span>Итого:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>12900 р.</b>
      </div>

      <div class="flex gap-2">
        <span>Налог:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>5%</b>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
