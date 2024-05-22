<template>
  <header
    class="bg-gradient-to-r from-blue-500 to-purple-600 shadow h-16 flex justify-between items-center px-5"
  >
    <router-link
      :to="{ name: 'home' }"
      class="inline-flex items-center h-full px-5 text-white font-bold text-lg tracking-wide transition-colors duration-300 hover:text-yellow-300"
    >
      Home
    </router-link>
    <div class="flex items-center gap-4">
      <router-link
        :to="{ name: 'byName' }"
        class="inline-flex items-center px-3 h-full text-white font-semibold text-base tracking-wide transition-colors duration-300 hover:bg-yellow-300 hover:text-blue-900 rounded-md"
      >
        Search Meals
      </router-link>
      <router-link
        :to="{ name: 'byLetter' }"
        class="inline-flex items-center px-3 h-full text-white font-semibold text-base tracking-wide transition-colors duration-300 hover:bg-yellow-300 hover:text-blue-900 rounded-md"
      >
        Meals By Letter
      </router-link>
      <router-link
        :to="{ name: 'byIngredient' }"
        class="inline-flex items-center px-3 h-full text-white font-semibold text-base tracking-wide transition-colors duration-300 hover:bg-yellow-300 hover:text-blue-900 rounded-md"
      >
        Meals By Ingredients
      </router-link>
    </div>
  </header>
</template>
