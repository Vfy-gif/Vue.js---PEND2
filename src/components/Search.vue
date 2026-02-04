<script setup lang="ts">
import { ref } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();
const racaDigitada = ref("");
const mensagemErro = ref("");

function irParaResultado() {
  if (racaDigitada.value) {
    mensagemErro.value = "";
    router.push(`/resultado/${racaDigitada.value.toLowerCase()}`);
  } else {
    mensagemErro.value = "Por favor, digite o nome de uma raça!";
  }
}
</script>

<template>
  <div class="logo">
    <h1>DogAPI</h1>
    <img src="../assets/dog-api-logo.svg" />
  </div>
  <div class="search">
    <input
      v-model="racaDigitada"
      type="text"
      placeholder="Digite uma raça"
      @keydown.enter="irParaResultado"
    />
    <button @click="irParaResultado">
      <div class="buscar"><img src="../assets/Search.svg" /></div>
    </button>
  </div>
  <h2 v-if="mensagemErro" class="erro-texto">
    {{ mensagemErro }}
  </h2>
</template>

<style>
.erro-texto {
  color: red;
  text-align: center;
  margin-top: 10px;
  font-family: sans-serif;
  font-size: 16px;
}

.search {
  display: flex;
  justify-content: center;
  align-items: center;
  padding-top: 5vh;
  position: relative;
  display: flex;
  flex-wrap: wrap;
}

input {
  background-color: rgba(185, 185, 185, 1);
  border: 0;
  outline: 0;
  height: 45px;
  width: 40vw;
  text-indent: 14px;
  font-size: 15px;
  border-radius: 20px;
  box-shadow: 5px 5px 10px #333;
  transition: 0.6s;
}

input:hover {
  background-color: rgba(148, 148, 148, 1);
}
input::placeholder {
  color: rgba(24, 24, 24, 0.8);
}

button {
  height: 45px;
  width: 45px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(255, 255, 255, 0.616);
  border-left: 3px solid blue;
  border: 0;
  border-radius: 20px;
  position: absolute;
  margin-left: 37vw;
  transition: 0.6s;
}

button:hover {
  background-color: rgba(117, 68, 196, 0.753);
}
.buscar {
  margin-top: -5px;
  height: 45px;
  width: 45px;
}
img {
  height: 100%;
  width: 100%;
}

.logo {
  height: 300px;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
  font-size: 30px;
  font-family: sans-serif;
}

.logo img {
  height: 160px;
  width: 160px;
}
</style>
