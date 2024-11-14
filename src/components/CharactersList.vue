<template>
  <div>
    <!-- Exibe o cartão do personagem selecionado, mostrando a imagem e o nome -->
    <CharacterSelected
      v-if="selectedCharacter"
      :image="selectedCharacter.image"
      :name="selectedCharacter.name"
      :species="selectedCharacter.species"
      :gender="selectedCharacter.gender"
      :dateOfBirth="selectedCharacter.dateOfBirth"
      :hogwartsStudent="selectedCharacter.hogwartsStudent"
      :hogwartsStaff="selectedCharacter.hogwartsStaff"
      :wizard="selectedCharacter.wizard"
      :alive="selectedCharacter.alive"
    />

    <!-- Exibe animação de carregamento enquanto 'loading' for verdadeiro -->
    <div v-if="loading" class="loading-container">
      <div class="loader"></div>
    </div>

    <!-- Container centralizado para a lista de personagens -->
    <div v-if="!loading" class="container col-12 mt-4 text-center w-100" id="lista">
      <!-- Barra de pesquisa para filtrar personagens -->

      <div class="input-group col-12">
        <div class="row col-8">
          <input
            type="text"
            class="form-control mt-4"
            placeholder="Busque um personagem..."
            v-model="searchTerm"
            id="barradepesquisa"
          />
        </div>
      </div>

      <!-- Lista de personagens filtrados com base na pesquisa -->
      <div class="container text-center col-12 mt-4 p-1">
        <ul class="row w-100" id="lista">
          <!-- Itera sobre os personagens filtrados na variável filteredCharacters -->
          <li
            v-for="character in filteredCharacters"
            :key="character.id"
            class="col-lg-4 col-md-6 col-sm-6"
          >
            <!-- Chama a função para selecionar o personagem ao clicar no cartão -->
            <div class="card mt-4 p-2" @click="selectCharacter(character)">
              <div class="card-body">
                <img
                  :src="character.image"
                  class="card-img-top w-50"
                  id="listImage"
                />
                <!-- Nome do personagem -->
                <h5 class="card-title">{{ character.name }}</h5>
                <!-- Casa do personagem -->
                <p class="card-text">
                  <strong>House: </strong> {{ character.house || 'No house' }}
                </p>
                <!-- Espécie do personagem -->
                <p class="card-text">
                  <strong>Species: </strong> {{ character.species }}
                </p>
              </div>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
// Importações necessárias do Vue
import { ref, onMounted, computed } from 'vue'
import CharacterSelected from './CharacterSelected.vue'

export default {
  name: 'CharactersList',
  // Declaração do componente CharacterSelected como um componente filho
  components: {
    CharacterSelected,
  },
  setup() {
    const characters = ref([]) // Lista de todos os personagens
    const loading = ref(true) // Estado de carregamento da API
    const error = ref(null) // Armazena mensagens de erro, se houver
    const selectedCharacter = ref(null) // Armazena o personagem selecionado
    const searchTerm = ref('') // Termo de pesquisa para filtrar personagens

    // Função para buscar dados da API de personagens
    const fetchCharacters = async () => {
      try {
        // Requisição para obter as informações dos personagens
        const response = await fetch(
          'https://hp-api.onrender.com/api/characters'
        )
        if (!response.ok) {
          throw new Error('Erro ao buscar dados.') // Lança um erro se a resposta não for ok
        }
        // Obtém todos os personagens e limita a lista aos primeiros 21
        const allCharacters = await response.json()
        characters.value = allCharacters.slice(0, 21)
      } catch (err) {
        error.value = err.message // Armazena a mensagem de erro
      } finally {
        loading.value = false // Atualiza o estado de carregamento
      }
    }

    // Função para selecionar um personagem quando o cartão é clicado
    const selectCharacter = character => {
      selectedCharacter.value = character
      window.scrollTo({ top: 0, behavior: 'smooth' })
    }

    // Computed para filtrar personagens baseado no termo de pesquisa
    const filteredCharacters = computed(() => {
      return characters.value.filter(character =>
        character.name.toLowerCase().includes(searchTerm.value.toLowerCase())
      )
    })

    // Busca os personagens assim que o componente é montado
    onMounted(fetchCharacters)

    return {
      characters,
      loading,
      error,
      selectedCharacter,
      selectCharacter,
      searchTerm,
      filteredCharacters,
    }
  },
}
</script>

<style>
CharacterSelected #lista {
  background-color: #101d0d;
}

li {
  list-style: none;
}

img {
  height: 10rem;
  object-fit: contain;
}

#listImage:hover {
  cursor: pointer;
  transition: 0.5s;
  transform: scale(95%);
}

#lista .card:hover {
  transition: 0.5s;
  background-color: #272f24;
}

#lista .card .card-title {
  margin-top: 0.5rem;
}

.input-group {
  align-items: center;
  justify-content: center;
}

.card {
  border: 0;
  background-color: #162213;

  color: white;

  box-shadow: #101d0d;
}

#barradepesquisa {
  background-color: #162213;
  border-color: black;
  border: 2rem;
  color: white;
}

.input-group ::placeholder {
  color: white;
}

/* HTML: <div class="loader"></div> */
.loader {
  width: 90px;
  height: 14px;
  background: radial-gradient(circle closest-side, #000 92%, #0000)
    calc(100% / 3) 0 / calc(100% / 4) 100%;
  animation: l2 0.5s infinite linear;
}
@keyframes l2 {
  100% {
    background-position: 0 0;
  }
}

.loading-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  position: absolute;
  width: 100%;
  top: 0;
  left: 0;
  background-color: rgba(0, 0, 0, 0.2);
  z-index: 1000;
}

</style>
