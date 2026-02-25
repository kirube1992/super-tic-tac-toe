<script setup>
import { ref } from "vue";

const grid = ref([
  [null, null, null],
  [null, null, null],
  [null, null, null],
]);

const gameStarted = ref(false);
const firstPlayer = ref("");
const secondPlayer = ref("");
const currentPlayer = ref("");
const winner = ref(null);

function checkWinner() {
  const g = grid.value;

  for (let i = 0; i < 3; i++) {
    if (g[i][0] && g[i][0] === g[i][1] && g[i][1] === g[i][2]) return g[i][2];
  }

  for (let i = 0; i < 3; i++) {
    if (g[0][i] && g[0][i] === g[1][i] && g[1][i] === g[2][i]) return g[2][i];
  }

  if (g[0][0] && g[0][0] === g[1][1] && g[1][1] === g[2][2]) return g[2][2];
  if (g[0][2] && g[0][2] === g[1][1] && g[1][1] === g[2][0]) return g[2][0];

  if (!g.flat().includes(null)) return "Draw";

  return null;
}
function startGame(choice) {
  firstPlayer.value = choice;
  secondPlayer.value = choice === "X" ? "O" : "X";
  currentPlayer.value = choice;
  gameStarted.value = true;
  winner.value = null;
}

function makeAMove(row, col) {
  if (gameStarted.value && grid.value[row][col] === null && !winner.value) {
    grid.value[row][col] = currentPlayer.value;

    const result = checkWinner();

    if (result) {
      winner.value = result;
    } else {
      currentPlayer.value = currentPlayer.value === "X" ? "O" : "X";
    }
  }
}

function resetGame() {
  grid.value = [
    [null, null, null],
    [null, null, null],
    [null, null, null],
  ];
  winner.value = null;
  gameStarted.value = false;
  currentPlayer.value = "";
}
</script>

<template>
  <div class="container">
    <h1>Welocome to tac toy</h1>
    <h2>player one which letter you wnat use to play?</h2>
    <div v-if="!gameStarted" class="setup">
      <button @click="startGame('X')">X</button>
      <button @click="startGame('O')">O</button>
    </div>

    <div v-else class="game-area">
      <div v-if="winner">
        <h2 v-if="winner === 'Draw'" class="status">It's a Draw! 😐</h2>
        <h2 v-else class="status winner">Winner: Player {{ winner }}! 🎉</h2>
        <button @click="resetGame" class="reset-btn">Play Again / Reset</button>
      </div>

      <h2 class="Main-intro">current player {{ currentPlayer }}</h2>
      <div v-for="(row, rowIndex) in grid" :key="rowIndex" class="row">
        <button
          v-for="(cell, coinIndex) in row"
          type="text"
          :key="coinIndex"
          @click="makeAMove(rowIndex, coinIndex)"
          class="cell"
          :class="{ 'is-x': cell === 'X', 'is-o': cell === 'O' }"
        >
          {{ cell }}
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  text-align: center;
  font-family: sans-serif;
}
.status {
  font-size: 1.8rem;
  margin: 10px;
}
.winner {
  color: green;
  font-weight: bold;
}

.row {
  display: flex;
  justify-content: center;
}
.cell {
  width: 60px;
  height: 60px;
  margin: 2px;
  font-size: 1.5rem;
  font-weight: bold;
  cursor: pointer;
  background-color: #eee;
  border: 1px solid #ccc;
}

.is-x {
  color: red;
}
.is-o {
  color: blue;
}

.reset-btn {
  margin-bottom: 20px;
  padding: 10px 20px;
  cursor: pointer;
  background-color: #333;
  color: white;
  border: none;
}
</style>
