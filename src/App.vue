<script setup>
import { computed, provide, ref, watch } from 'vue'

import AppHeader from '@/components/AppHeader.vue'
import Drawer from '@/components/Drawer.vue'

const cart = ref([])
const drawerOpen = ref(false)

const totalPrice = computed(() =>
  cart.value.reduce((acc, item) => acc + item.price, 0),
)

const vatPrice = computed(() => Math.round((totalPrice.value * 5) / 100))

const closeDrawer = () => {
  drawerOpen.value = false
}

const openDrawer = () => {
  drawerOpen.value = true
}

const removeFromCart = item => {
  item.isAdded = false
  cart.value.splice(cart.value.indexOf(item), 1)
}

const addToCart = item => {
  item.isAdded = true
  cart.value.push(item)
}

watch(
  cart,
  () => {
    localStorage.setItem('cart', JSON.stringify(cart.value))
  },
  { deep: true },
)

provide('cartActions', {
  cart,
  openDrawer,
  closeDrawer,
  removeFromCart,
  addToCart,
})
</script>

<template>
  <Drawer v-if="drawerOpen" :total-price="totalPrice" :vat-price="vatPrice" />
  <div class="w-4/5 m-auto bg-white rounded-xl shadow-xl mt-14 mb-14">
    <AppHeader :total-price="totalPrice" @open-drawer="openDrawer" />
    <div class="p-10">
      <RouterView />
    </div>
  </div>
</template>
