<script setup>
import { ref } from "vue";

const firstPlayer = ref("");
const secondPlayer = ref("");
const currentPlayer = ref("");
const winner = ref(false);

const grid = ref([
  [null, null, null],
  [null, null, null],
  [null, null, null],
]);

function checkWinner() {
  const g = grid.value;
  for (let i = 0; i < 3; i++) {
    if (g[i][0] && g[i][0] === g[i][1] && g[i][1] === g[i][2]) return g[i][2];
  }
  for (let i = 0; i < 3; i++) {
    if (g[0][i] && g[0][i] === g[1][i] && g[1][i] === g[2][i]) return g[i][2];
  }

  if (g[0][0] && g[0][0] === g[1][1] && g[1][1] === g[2][2]) return g[2][2];
  if (g[0][2] && g[0][2] === g[1][1] && g[1][1] === g[2][0]) return g[2][0];

  if (!g.flat().includes(null)) return "Draw";
  return;
}

function makeAMove(row, col) {
  if (grid.value[row][col] === null) {
    grid.value[row][col] = currentPlayer.value;

    const result = checkWinner();

    if (result) {
      winner.value = result;
    } else {
      currentPlayer.value = currentPlayer.value === "X" ? "O" : "X";
    }
  }
}

function preferletter(choise) {
  firstPlayer.value = choise;
  secondPlayer.value = choise === "X" ? "O" : "X";
  currentPlayer.value = choise;
}
</script>
<template>
  <div class="container">
    <h2>Welcome to tic tac toe</h2>
    <div>
      <p>which letter you preffer to play with</p>
      <button class="btn" @click="preferletter('X')">X</button>
      <button class="btn" @click="preferletter('O')">O</button>
      <h2>current player is {{ currentPlayer }}</h2>
    </div>
    <div class="winner" v-if="winner">
      <h2 v-if="winner === 'Draw'">it's Draw</h2>
      <h2 v-else>winner: player{{ winner }}</h2>
    </div>
    <div v-for="(row, rowIndex) in grid" :key="rowIndex" class="row">
      <button
        v-for="(cell, cellIndex) in row"
        type="text"
        :key="cellIndex"
        @click="makeAMove(rowIndex, cellIndex)"
        class="cell"
        :class="{ 'is-X': cell === 'X', 'is-O': cell === 'O' }"
      >
        {{ cell }}
      </button>
    </div>
  </div>
</template>

<style>
.container {
  text-align: center;
  font-family: sans-serif;
}

.row {
  display: flex;
  justify-content: center;
}

.btn {
  height: 60px;
  width: 60px;
  margin: 0.2px;
}

.cell {
  width: 60px;
  height: 60px;
  margin: 2px;
  cursor: pointer;
}
.is-X {
  color: red;
}
.is-O {
  color: blue;
}
</style>
