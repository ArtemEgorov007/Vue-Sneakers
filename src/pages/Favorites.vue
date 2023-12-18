<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

import CardList from '../components/CardList.vue'

const favorites = ref([])

onMounted(async () => {
  try {
    const { data } = await axios.get(
      'https://da04fcb380658a35.mokky.dev/favorites?_relations=items'
    )

    favorites.value = data.map((obj) => obj.item)
  } catch (err) {
    console.log(err)
  }
})
</script>

<template>
  <div>
    <h2 class="text-3xl font-bold mb-8">Мои закладки</h2>

    <template v-if="favorites.length > 0">
      <CardList :items="favorites" is-favorites />
    </template>
    <template v-else>
      <p>В избранном ничего нет.</p>
    </template>
  </div>
</template>
