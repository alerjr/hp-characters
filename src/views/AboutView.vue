<script setup>
import Navbar from '../components/Navbar.vue'
import Footer from '../components/Footer.vue'
import { RouterLink } from 'vue-router'

const s = window.scrollTo({ top: 0, behavior: 'smooth' })
</script>

<template>
  <div>
    <Navbar />
    <div v-if="!loading" class="container d-flex justify-content-center mt-5 mb-2">
      <div class="card" style="width: 32rem">
        <img
          src="../assets/pexels-mikhail-nilov-8390268.jpg"
          class="card-img-top"
          alt="..."
        />
        <div class="card-body">
          <h3 class="card-title">Projeto Harry Potter</h3>
          <hr />
          <div>
            <h5 class="card-title">Descrição</h5>
            <p class="card-text">
              Esse projeto é uma aplicação web construída a partir do Vue que
              tem mostra as mais variadas informações sobre diversos personagens
              do universo Harry Potter, como nome, data de nascimento, casa
              pertencente, etc.
            </p>
            <hr />
          </div>

          <div>
            <h5 class="card-title">Objetivo</h5>
            <p class="card-text">
              O objetivo deste projeto é exibir de forma dinâmica e simplificada
              tais informações, que são obtidas através de uma API já pronta com
              esses dados para consulta.
            </p>
            <hr />
          </div>

          <div>
            <h5 class="card-title">Tecnologias/frameworks utilizadas(os):</h5>

            <ul class="list-group list-group-flush">
              <li class="list-group-item">HTML</li>
              <li class="list-group-item">CSS</li>
              <li class="list-group-item">Javascript</li>
              <li class="list-group-item">Vue</li>
              <li class="list-group-item">Bootstrap</li>
            </ul>
          </div>
        </div>

        <div
          class="card-body d-flex justify-content-around text-center"
          id="aboutFooter"
        >
          <router-link to="/" class="card-link text-center" @click="s">
            Página do projeto</router-link
          >
          <a
            href="https://github.com/alerjr"
            class="card-link text-center"
            target="”_blank”"
            >Github <span><img src="../assets/github.svg" style="width: 24px; height: 24px; object-fit: contain;"></span></a
          >
        </div>
      </div>
    </div>
    <Footer />
  </div>
</template>

<style scoped>
.list-group .list-group-flush li {
  background-color: #162213;
  color: white;
}

.card {
  box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 12px;
}

ul li:hover {
  background-color: #2557191a;
}

ul li {
  background-color: #162213;
  color: white;
}

#aboutFooter a {
  color: white;
  text-decoration: none;
}

#aboutFooter a:hover {
  color: rgba(255, 255, 255, 0.526);
}

.card-img-top {
  width: 100%;
  object-fit: cover;
  object-position: center;
}
</style>
