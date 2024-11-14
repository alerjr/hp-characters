<template>
  <!-- Container centralizado -->
  <div class="container d-flex justify-content-center">
    <!-- Card do personagem selecionado -->
    <div class="card mt-4" style="width: 32rem" id="lista">
      <!-- Imagem do personagem -->
      <img
        :src="image"
        class="card-img-top p-2"
        id="imagem"
        alt="Foto de {{name}}"
      />
      <div class="card-body">
        <!-- Nome do personagem -->
        <h5 class="card-title">{{ name }}</h5>
        <!-- Descricao do personagem  -->
        <p class="card-text">
          {{ species.toString().capitalize() }}, {{ gender }},
          {{
            dateOfBirth
              ? 'born in ' + dateOfBirth.replaceAll('-', '/')
              : 'no birth date'
          }}
        </p>

        <p class="card-text" v-if="hogwartsStaff"><strong>Staff</strong></p>
        <p class="card-text" v-else-if="hogwartsStudent">
          <strong>Student</strong>
        </p>

        <p class="card-text" v-if="alive">
          Alive:
          <img
            src="../../src/assets/check-circle-svgrepo-com.svg"
            class="ifIcon"
          />
        </p>
        <p class="card-text" v-else-if="!alive">
          Alive:
          <img
            src="../../src/assets/cross-circle-svgrepo-com.svg"
            class="ifIcon"
          />
        </p>

        <p class="card-text" v-if="wizard">
          Wicked:
          <img
            src="../../src/assets/check-circle-svgrepo-com.svg"
            class="ifIcon"
          />
        </p>
        <p class="card-text" v-else-if="!wizard">
          Wicked:
          <img
            src="../../src/assets/cross-circle-svgrepo-com.svg"
            class="ifIcon"
          />
        </p>
      </div>
    </div>
  </div>
</template>

<script>
// convert case
Object.defineProperty(String.prototype, 'capitalize', {
  value: function () {
    return this.charAt(0).toUpperCase() + this.slice(1)
  },
  enumerable: false,
})

export default {
  name: 'CharacterSelected',
  data() {
    return {
      dateOfBirth: '', // Altere para uma data válida ou mantenha vazio
    }
  },
  // Props de imagem e nome
  props: {
    image: {
      type: String,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    species: {
      type: String,
      required: true,
    },
    gender: {
      type: String,
      required: true,
    },
    dateOfBirth: {
      type: String,
      required: true,
    },
    hogwartsStudent: {
      type: undefined,
      required: true,
    },
    hogwartsStaff: {
      type: undefined,
      required: true,
    },
    wizard: {
      type: undefined,
      required: true,
    },
    alive: {
      type: undefined,
      required: true,
    },
  },
}
</script>

<style>
.ifIcon {
  width: 1rem;
  height: 1rem;
}
</style>