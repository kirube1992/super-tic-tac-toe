<script setup>
import { ref } from "vue";
import welcome from "./welcome.vue";

const currentPlayer = ref("");
const winner = ref(false);

const grid = ref([
  [
    [
      [null, null, null],
      [null, null, null],
      [null, null, null],
    ],
    [
      [null, null, null],
      [null, null, null],
      [null, null, null],
    ],
    [
      [null, null, null],
      [null, null, null],
      [null, null, null],
    ],
  ],
  [
    [
      [null, null, null],
      [null, null, null],
      [null, null, null],
    ],
    [
      [null, null, null],
      [null, null, null],
      [null, null, null],
    ],
    [
      [null, null, null],
      [null, null, null],
      [null, null, null],
    ],
  ],
  [
    [
      [null, null, null],
      [null, null, null],
      [null, null, null],
    ],
    [
      [null, null, null],
      [null, null, null],
      [null, null, null],
    ],
    [
      [null, null, null],
      [null, null, null],
      [null, null, null],
    ],
  ],
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

function makeAMove(bigrow, bigcol, smallrow, smallcoloumn) {
  if (grid.value[bigrow][bigcol][smallrow][smallcoloumn] === null) {
    grid.value[bigrow][bigcol][smallrow][smallcoloumn] = currentPlayer.value;

    const result = checkWinner();

    if (result) {
      winner.value = result;
    } else {
      currentPlayer.value = currentPlayer.value === "X" ? "O" : "X";
    }
  }
}
</script>
<template>
  <welcome />
  <div class="container">
    <div class="winner" v-if="winner">
      <h2 v-if="winner === 'Draw'">it's Draw</h2>
      <h2 v-else>winner: player{{ winner }}</h2>
    </div>
    <div class="box-container">
      <div
        v-for="(bigrow, bigrowIndex) in grid"
        :key="bigrowIndex"
        class="bigrow"
      >
        <div
          v-for="(smallBord, smallBordIndex) in bigrow"
          class="smallBord"
          :key="smallBordIndex"
        >
          <div v-for="(row, rowindex) in smallBord" :key="rowindex" class="row">
            <button
              v-for="(cell, cellIndex) in row"
              type="button"
              :key="cellIndex"
              @click="
                makeAMove(bigrowIndex, smallBordIndex, rowindex, cellIndex)
              "
              class="cell"
              :class="{ 'is-X': cell === 'X', 'is-O': cell === 'O' }"
            >
              {{ cell }}
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
}

.box-container {
  border: 3px solid #333;
}
.bigrow {
  display: flex;
  margin: 5px;
}

.smallBord {
  display: flex;
  flex-direction: column;
  border: 3px solid #333;
  margin: 5px;
  padding: 5px;
  background-color: #f0f0f0;
}

.cell {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  margin: 2px;
  border: 1px solid #999;
  background-color: white;
  font-size: 20px;
  font-weight: bold;
  cursor: pointer;
  align-items: center;
  padding: 0;
  line-height: 1;
  box-sizing: border-box;
}

.row {
  display: flex;
  flex: 0 0 33.33%;
  box-sizing: border-box;
  text-align: center;
}

.cell:hover {
  background-color: #f5f5f5;
}

.is-X {
  color: red;
}
.is-O {
  color: blue;
}
</style>
