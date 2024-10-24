<script setup>
import AppHeader from '@/components/AppHeader.vue'
import CardList from '@/components/CardList.vue'
import Drawer from '@/components/Drawer.vue'
</script>

<template>
  <div class="w-4/5 m-auto bg-white rounded-xl shadow-xl mt-14 mb-14">
    <Drawer />
    <AppHeader />
    <div class="p-10">
      <h2 class="text-4xl font-bold mb-8">Все кроссовки</h2>
      <CardList />
    </div>
  </div>
</template>
