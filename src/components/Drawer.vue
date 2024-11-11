<script setup>
import DrawerHeader from '@/components/DrawerHeader.vue'
import CartListItem from '@/components/CartListItem.vue'
import { computed, inject, ref } from 'vue'
import Info from '@/components/Info.vue'
import axios from 'axios'

const props = defineProps({
  totalPrice: Number,
  vatPrice: Number,
})
const isCreatingOrder = ref(false)
const orderItemId = ref(null)

const { cart } = inject('cartActions')

const createOrder = async () => {
  try {
    isCreatingOrder.value = true
    const { data } = await axios.post(
      'https://fd192f320b005090.mokky.dev/orders',
      {
        items: cart.value,
        totalPrice: props.totalPrice,
      },
    )

    cart.value = []
    orderItemId.value = data.id
    return data
  } catch (e) {
    console.error(e)
  } finally {
    isCreatingOrder.value = false
  }
}

const buttonDisabled = computed(
  () => isCreatingOrder.value || !props.totalPrice,
)
</script>

<template>
  <div class="fixed top-0 left-0 bg-black h-full w-full z-10 opacity-65"></div>
  <div class="bg-white h-full w-96 right-0 top-0 z-20 p-8 fixed">
    <DrawerHeader />
    <div v-if="!totalPrice || orderItemId" class="flex h-full items-center">
      <Info
        v-if="orderItemId"
        :description="`Ваш заказ №${orderItemId} скоро будет передан курьерской доставке.`"
        image-url="/order-success-icon.png"
        title="Заказ оформлен!"
      />

      <Info
        v-if="!totalPrice && !orderItemId"
        description="Добавьте хотя бы одну пару кроссовок, чтобы сделать заказ"
        image-url="/cart-empty.png"
        title="Корзина пустая"
      />
    </div>

    <div v-else>
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
          @click="createOrder"
        >
          Оформить заказ
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
