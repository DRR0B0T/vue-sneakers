<script setup></script>

<template>
  <div class="w-4/5 m-auto bg-white h-screen rounded-xl shadow-xl mt-14 mb-14">
    <header
      class="bg-white flex items-center justify-between border-b border-slate-300 px-8"
    >
      <div class="flex items-center gap-4">
        <img alt="Logo" class="w-10" src="/logo.png" />
        <div>
          <h2 class="text-xl font-bold uppercase">Vue Sneakers</h2>
          <p>Магазин самых лучших кроссовок</p>
        </div>
      </div>
      <ul>
        <li>
          <img alt="Cart" src="/cart.svg" />
          <b>1205 руб.</b>
        </li>
        <li>
          <img alt="Heart" src="/heart.svg" />
          <b>Закладки</b>
        </li>
        <li>
          <img alt="Profile" src="/profile.svg" />
          <b>Профиль</b>
        </li>
      </ul>
    </header>
    <h1>Ilmir Mavliutov</h1>
  </div>
</template>

<style scoped>
.layout {
  display: flex;
  flex-direction: column;
}
</style>
