<script setup>
import CardList from '@/components/CardList.vue'
import axios from 'axios'
import debounce from 'lodash.debounce'
import { inject, onMounted, reactive, ref, watch } from 'vue'

const items = ref([])
const filters = reactive({
  sortBy: 'title',
  searchQuery: '',
})

const { removeFromCart, addToCart, cart } = inject('cartActions')

const onChangeSelect = e => {
  filters.sortBy = e.target.value
}

const onInputSearch = debounce(e => {
  filters.searchQuery = e.target.value
}, 500)

const onFavoriteAdd = async item => {
  try {
    if (!item.isFavorite) {
      const params = {
        item_id: item.id,
      }
      item.isFavorite = true

      const { data } = await axios.post(
        `https://fd192f320b005090.mokky.dev/favorites`,
        params,
      )

      item.favoriteId = data.id
    } else {
      item.isFavorite = false

      await axios.delete(
        `https://fd192f320b005090.mokky.dev/favorites/${item.favoriteId}`,
      )
    }
  } catch (e) {
    console.error(e)
  }
}

const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get(
      `https://fd192f320b005090.mokky.dev/favorites`,
    )

    items.value = items.value.map(item => {
      const favorite = favorites.find(fav => fav.item_id === item.id)
      if (!favorite) {
        return item
      }

      return {
        ...item,
        isFavorite: true,
        favoriteId: favorite.id,
      }
    })
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
      favoriteId: null,
      isAdded: false,
    }))
  } catch (e) {
    console.error(e)
  }
}

const onAddToCart = item => {
  if (!item.isAdded) {
    addToCart(item)
  } else {
    removeFromCart(item)
  }
}

onMounted(async () => {
  const localCart = localStorage.getItem('cart')
  cart.value = localCart ? JSON.parse(localCart) : []

  await fetchData()
  await fetchFavorites()
  items.value = items.value.map(item => ({
    ...item,
    isAdded: cart.value.some(cartItem => cartItem.id === item.id),
  }))
})

watch(cart, () => {
  items.value = items.value.map(item => ({
    ...item,
    isAdded: false,
  }))
})

watch(filters, fetchData)
</script>

<template>
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
  <CardList
    :items="items"
    @on-add-to-cart="onAddToCart"
    @on-favorite-add="onFavoriteAdd"
  />
</template>
