<script setup>
import CartItem from '@/components/CartItem.vue'
import { inject } from 'vue'

const { cart, removeFromCart } = inject('cartActions')
</script>

<template>
  <div v-auto-animate class="flex flex-1 flex-col gap-4">
    <CartItem
      v-for="item in cart"
      :key="item.id"
      :image-url="item.imageUrl"
      :price="item.price"
      :title="item.title"
      @on-click-remove="() => removeFromCart(item)"
    />
  </div>
</template>

<style scoped></style>
