<template>
  <div class="p-8 pb-0">
    <h1
      class="text-4xl font-bold mb-4 text-blue-500 flex justify-center items-center"
    >
      Search Meals by Ingredients
    </h1>
  </div>
  <div class="px-8">
    <input
      type="text"
      v-model="keyword"
      class="rounded-lg border-2 bg-white border-gray-300 focus:ring-blue-500 focus:border-blue-500 mb-5 w-full p-3"
      placeholder="Search for Ingredients"
    />
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
      <div
        v-for="ingredient in computedIngredients"
        :key="ingredient.idIngredient"
        class="block bg-white rounded-lg p-5 shadow-lg transition transform hover:scale-105"
      >
        <h3 class="text-2xl font-bold mb-2 text-gray-800">
          {{ ingredient.strIngredient }}
        </h3>
        <p class="text-gray-600 mb-2">
          {{
            isReadMoreVisible(ingredient.idIngredient)
              ? ingredient.strDescription
              : truncatedDescription(ingredient.strDescription)
          }}
          <span
            v-if="showReadMore(ingredient.strDescription)"
            @click="toggleReadMore(ingredient.idIngredient)"
            class="text-blue-500 cursor-pointer"
          >
            {{
              isReadMoreVisible(ingredient.idIngredient)
                ? 'read less'
                : '...read more'
            }}
          </span>
        </p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, ref } from 'vue';
import { onMounted } from 'vue';
import axiosClient from '../axiosClient';

const keyword = ref('');
const ingredients = ref([]);
const readMoreStates = ref({});

const computedIngredients = computed(() => {
  if (!keyword.value) return ingredients.value;
  return ingredients.value.filter((i) =>
    i.strIngredient.toLowerCase().includes(keyword.value.toLowerCase())
  );
});

function truncatedDescription(description) {
  if (!description) return 'No description available.';
  const words = description.split(' ');
  if (words.length <= 50) return description;
  return words.slice(0, 50).join(' ');
}

function showReadMore(description) {
  return description && description.split(' ').length > 50;
}

function toggleReadMore(id) {
  readMoreStates.value[id] = !readMoreStates.value[id];
}

function isReadMoreVisible(id) {
  return readMoreStates.value[id];
}

onMounted(() => {
  axiosClient.get('list.php?i=list').then(({ data }) => {
    ingredients.value = data.meals;
  });
});
</script>
