<script setup>
import CartItem from '@/components/CartItem.vue'
import { inject } from 'vue'

const { cart } = inject('cartActions')
</script>

<template>
  <div class="flex flex-1 flex-col gap-4">
    <CartItem
      v-for="item in cart"
      :key="item.id"
      :imageUrl="item.imageUrl"
      :price="item.price"
      :title="item.title"
    />
  </div>
</template>

<style scoped></style>
