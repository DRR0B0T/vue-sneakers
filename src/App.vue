<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'

import AppHeader from '@/components/AppHeader.vue'
import CardList from '@/components/CardList.vue'

const items = ref([])

onMounted(async () => {
  try {
    const { data } = await axios.get('https://fd192f320b005090.mokky.dev/items')
    items.value = data
  } catch (e) {
    console.error(e)
  }
})
</script>

<template>
  <div class="w-4/5 m-auto bg-white rounded-xl shadow-xl mt-14 mb-14">
    <!--    <Drawer />-->
    <AppHeader />
    <div class="p-10">
      <div class="flex justify-between items-center">
        <h2 class="text-4xl font-bold mb-8">Все кроссовки</h2>

        <div class="flex gap-4">
          <select
            class="py-2 px-3 border rounded-md outline-none cursor-pointer"
          >
            <option value="1">По названию</option>
            <option value="2">По цене (дешёвые)</option>
            <option value="3">По цене (дорогие)</option>
          </select>

          <div class="relative">
            <img alt="Search" class="absolute left-4 top-3" src="/search.svg" />
            <input
              class="border rounded-md py-2 pl-11 pr-4 outline-none focus:border-gray-400"
              placeholder="Поиск..."
              type="text"
            />
          </div>
        </div>
      </div>
      <CardList :items="items" />
    </div>
  </div>
</template>
