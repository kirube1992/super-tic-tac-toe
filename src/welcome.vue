<script setup>
import { ref } from "vue";

const firstPlayer = ref("");
const secondPlayer = ref("");
const currentPlayer = ref("");

function preferletter(choise) {
  firstPlayer.value = choise;
  secondPlayer.value = choise === "X" ? "O" : "X";
  currentPlayer.value = choise;
}
</script>

<template>
  <div class="contener">
    <h2 class="welcome-txt">Welcome to Super tic tac toe Game</h2>
    <div class="wel-input">
      <p>What is your name</p>
      <input placeholder="e.g. kirubel" />
    </div>

    <p>which letter you preffer to play with</p>
    <div class="welcome-page">
      <button class="letter-btn" @click="preferletter('X')">X</button>
      <button class="letter-btn" @click="preferletter('O')">O</button>
    </div>
    <h2>current player is {{ currentPlayer }}</h2>
  </div>
</template>

<style scoped>
.contener {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.welcome-txt {
  font-size: 50px;
}

.welcome-page {
  display: flex;
  gap: 10px;
}

.letter-btn {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100px;
  height: 100px;
}

.wel-input {
  display: flex;
  gap: 15px;
  padding: 5px;
  margin: 5px;
  border: 2px solid;
}
</style>
