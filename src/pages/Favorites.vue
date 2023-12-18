<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

import CardList from '../components/CardList.vue'

const favorites = ref([])

onMounted(async () => {
  try {
    const { data } = await axios.get(
      'https://604781a0efa572c1.mokky.dev/favorites?_relations=items'
    )

    favorites.value = data
      .filter((obj) => obj.item)
      .filter(
        (obj) =>
          !obj.item.isFavorite ||
          (obj.item.isFavorite && obj.item.favoriteId !== null && obj.item.isAdded)
      )
      .map((obj) => obj.item)
  } catch (err) {
    console.error(err)
  }
})
</script>

<template>
  <h2 class="text-3xl font-bold mb-8">Мои закладки</h2>

  <CardList :items="favorites" is-favorites />
</template>
