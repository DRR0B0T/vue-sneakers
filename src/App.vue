<script setup>
import { onMounted, reactive, ref, watch } from 'vue'
import axios from 'axios'

import AppHeader from '@/components/AppHeader.vue'
import CardList from '@/components/CardList.vue'

const items = ref([])
const filters = reactive({
  sortBy: 'title',
  searchQuery: '',
})

const onChangeSelect = e => {
  filters.sortBy = e.target.value
}

const onInputSearch = e => {
  filters.searchQuery = e.target.value
}

const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get(
      `https://fd192f320b005090.mokky.dev/favorites`,
    )

    items.value = items.value.map(item => {
      const favorite = favorites.find(fav => fav.parentId === item.id)
      if (!favorite) {
        return item
      }

      return {
        ...item,
        isFavorite: true,
        favoriteId: favorite.id,
      }
    })
    console.log(items.value)
  } catch (e) {
    console.error(e)
  }
}

const fetchData = async () => {
  try {
    const params = {
      sortBy: filters.sortBy,
    }

    if (filters.searchQuery) {
      params.title = `*${filters.searchQuery}*`
    }

    const { data } = await axios.get(
      `https://fd192f320b005090.mokky.dev/items`,
      { params },
    )

    items.value = data.map(obj => ({
      ...obj,
      isFavorite: false,
      isAdded: false,
    }))
  } catch (e) {
    console.error(e)
  }
}

onMounted(async () => {
  await fetchData()
  await fetchFavorites()
})

watch(filters, fetchData)
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
              @input="onInputSearch"
            />
          </div>
        </div>
      </div>
      <CardList :items="items" />
    </div>
  </div>
</template>
