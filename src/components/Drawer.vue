<script setup>
import DrawerHeader from '@/components/DrawerHeader.vue'
import CartListItem from '@/components/CartListItem.vue'
import { computed } from 'vue'

const emit = defineEmits(['createOrder'])

const props = defineProps({
  totalPrice: Number,
  vatPrice: Number,
  isCreatingOrder: Boolean,
})

const buttonDisabled = computed(
  () => props.isCreatingOrder || !props.totalPrice,
)
</script>

<template>
  <div class="fixed top-0 left-0 bg-black h-full w-full z-10 opacity-65"></div>
  <div class="bg-white h-full w-96 right-0 top-0 z-20 p-8 fixed">
    <DrawerHeader />
    <CartListItem />
    <div class="flex flex-col gap-5 mb-5 mt-6">
      <div class="flex gap-2">
        <span>Итого:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>{{ totalPrice }} р.</b>
      </div>

      <div class="flex gap-2">
        <span>Налог 5%:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>{{ vatPrice }} р.</b>
      </div>
      <button
        :disabled="buttonDisabled"
        class="mt-4 w-full rounded-xl bg-lime-500 py-5 text-white active:bg-lime-700 hover:bg-lime-600 cursor-pointer transition disabled:bg-slate-500"
        @click="emit('createOrder')"
      >
        Оформить заказ
      </button>
    </div>
  </div>
</template>

<style scoped></style>
