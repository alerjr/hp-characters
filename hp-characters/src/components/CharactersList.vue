<template>
  <div class="container col-8 text-center">
    <div class="card mt-4 row w-100">
      <div class="row">
        <h1 class="card-title col">Principal</h1>
        <h1 class="card-title col">Principal</h1>
      </div>
    </div>

    <ul class="row justify-content-between mt-4 col-12 p-2">
      <li
        class="col-lg-3 col-md-4 col-sm-12 card d-flex p-2"
        v-for="character in characters"
        :key="character.id"
      >
        <h3>{{ character.name }}</h3>
        <img
          :src="character.image"
          alt="Imagem de {{character.name}}"
          class="w-100"
        />
        <p class="mt-4"><strong>House: </strong> {{ character.house }}</p>
        <p><strong>Specie: </strong>{{ character.species }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue'

export default {
  name: 'CharacterList',
  setup() {
    const characters = ref([])

    const fetchCharacters = async () => {
      const response = await fetch('https://hp-api.onrender.com/api/characters')
      const allCharacters = await response.json()
      characters.value = allCharacters.slice(0, 20)
    }
    onMounted(fetchCharacters)

    return {
      characters,
    }
  },
}
</script>

<style scoped>
img {
  width: 150px;
  height: 150px;
  object-fit: contain;

  display: flex;
}

h3 {
  font-size: 20px;
  margin-top: 1rem;
  text-transform: uppercase;
  font-weight: 700;
}
</style>