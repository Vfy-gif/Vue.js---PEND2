<script setup>
"use strict";

import { ref } from "vue";

const cachorros = ref([])
const racaDigitada = ref("")

async function buscarImagens () {

  if (!racaDigitada.value) return;

    const url = `https://dog.ceo/api/breed/${racaDigitada.value.toLowerCase()}/images`
    const response  = await fetch(url)
    const imagens   =  await response.json()

    cachorros.value = imagens.message;
}

buscarImagens()

</script>

<template>
    <div class="search">
      <input v-model="racaDigitada" 
        type="text" 
        placeholder="Digite uma raça" 
        @keydown.enter="buscarImagens" />

      <button @click="buscarImagens">
        <div class="buscar">
          <div class="line"></div>
        </div>
      </button>
    </div>
    <div class="container" id="receber-dog">
      <img v-for="url in cachorros" :src="url"/>
    </div>
</template>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  height: 100vh;
  width: 100vw;
  background-color: rgb(74, 74, 173);
}

.search {
  display: flex;
  justify-content: center;
  align-items: center;
  padding-top: 5vh;
  position: relative;
}

input {
  border: 0;
  outline: 0;
  background-color: rgb(141, 141, 141);
  height: 45px;
  width: 26vw;
  text-indent: 14px;
  font-size: 15px;
  border-radius: 10px;
  transition: 0.6s;
}

input:hover {
  background-color: rgb(110, 110, 110);
}

button {
  height: 45px;
  width: 45px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(255, 255, 255, 0.616);
  border: 1px solid black;
  border-radius: 10px;
  position: absolute;
  margin-left: 23vw;
  transition: 0.6s;
}

button:hover {
  background-color: rgba(117, 68, 196, 0.753);
}
.buscar {
  margin-top: -5px;
  border-radius: 100px;
  border: 3px solid black;
  height: 23px;
  width: 23px;
}
.line {
  border: 2px solid black;
  margin-top: 14px;
  margin-left: 19px;
  transform: rotate(135deg);
  height: 10px;
  background-color: black;
}

.container {
  margin-top: 6vh;
  display: flex;
  flex-wrap: wrap;
  margin-inline: 10%;
}

.container img {
  height: 200px;
  width: 200px;
  object-fit: cover;
  transition: 0.6s;
}

.container a {
  height: 200px;
  width: 15vw;
  object-fit: cover;
}

.container img:hover {
  transform: scale(1.3);
}
</style>
