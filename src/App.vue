<script setup>
import { onMounted, ref, watch } from 'vue'
import axios from 'axios'

import AppHeader from '@/components/AppHeader.vue'
import CardList from '@/components/CardList.vue'

const items = ref([])
const filters = ref({
  sortBy: '',
  searchQuery: '',
})

const onChangeSelect = e => {
  filters.value.sortBy = e.target.value
}

onMounted(async () => {
  try {
    const { data } = await axios.get('https://fd192f320b005090.mokky.dev/items')
    items.value = data
  } catch (e) {
    console.error(e)
  }
})

watch(filters.value.sortBy, async () => {
  try {
    const { data } = await axios.get(
      'https://fd192f320b005090.mokky.dev/items?sortBy=' + filters.value.sortBy,
    )
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
            @change="onChangeSelect"
          >
            <option value="name">По названию</option>
            <option value="price">По цене (дешёвые)</option>
            <option value="-price">По цене (дорогие)</option>
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
