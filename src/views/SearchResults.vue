<script setup lang="ts">
import { ref, onMounted } from "vue";
import { useRoute, useRouter } from "vue-router";

const route = useRoute();
const router = useRouter();
const cachorros = ref([]);
const raca = route.params.raca;

async function buscarImagens() {
  try {
    const url = `https://dog.ceo/api/breed/${raca}/images`;
    const response = await fetch(url);
    const imagens = await response.json();

    if (imagens.status === "error") {
      alert("Raça não encontrada! Redirecionando...");
      router.push('/');
    } else {
      cachorros.value = imagens.message;
    }
  } catch (error) {
    router.push('/');
  }
}
onMounted(buscarImagens);
</script>

<template>
  <main>
    <div class="search-result">
    <nav>
      <button @click="router.push('/')"><img src="../assets/reply-arrow.svg"></button>
      <h2>Imagens de {{ raca }}</h2>
    </nav>
      <div class="container">
        <a v-for="url in cachorros" :key="url" :href="url" target="_blank">
          <img :src="url" />
        </a>
      </div>
    </div>
  </main>
</template>

<style>

.search-result {
  height: 100%;
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  font-size: 24px;
  font-family: sans-serif;
}

.search-result nav {
  display: flex;
  align-items: center;
  justify-content: center;
}

.search-result nav button {
  position: absolute;
  height: 80px;
  width: 80px;
  margin-left: -80%; 
}

nav button:hover {
  background-color: white;
  rotate: -50deg;
  transform: scale(1.5);
}

.container {
  margin-top: 6vh;
  display: flex;
  flex-wrap: wrap;
  justify-content: center; 
  gap: 10px;              
  width: 100%;
}

.container img {
  height: 100%;
  width: 100%;
  object-fit: cover;
  transition: 0.6s;
}

.container a {
  display: block;
  height: 200px;
  width: 200px;
  overflow: hidden;
}

.container img:hover {
  transform: scale(1.3);
}
</style>
