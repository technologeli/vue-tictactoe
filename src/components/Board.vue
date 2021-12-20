<script setup lang="ts">
import Cell from './Cell.vue';
import { reactive } from 'vue';
const board: number[][] = reactive([
  [0, 0, 0],
  [0, 0, 0],
  [0, 0, 0],
]);

let turn = 1; // player 1 (X) goes first

const play = (rowIdx: number, colIdx: number) => {
  board[rowIdx][colIdx] = turn;
  let hasWon = false;
  for (let i = 0; i < board.length; i++) {
    if (all(getRow(i), turn) || all) hasWon = true;
  }

  changePlayer();

}

const changePlayer = () => {
  if (turn === 1) turn = 2;
  else turn = 1;
}

const getRow = (idx: number) => {
  return board[idx];
}

const getCol = (idx: number) => {
  return board.map(row => row[idx]);
}

const getDiagonal = (topLeftToBottomRight: boolean) => {
  return board.map((row, idx) => {
    if (topLeftToBottomRight) return row[idx];
    else return row[board.length - 1 - idx]
  });
}

const all = (arr: number[], player: number) => {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] !== player) return false;
  }
  return true;
}

</script>

<template>
  <div class="bg-slate-600 rounded flex flex-col space-y-2 p-2">
    <div v-for="(row, rowIdx) in board" class="flex space-x-2">
      <Cell
        v-for="(col, colIdx) in row"
        :value="col"
        :row="rowIdx"
        :col="colIdx"
        :key="`${rowIdx} ${colIdx}`"
        @change="play(rowIdx, colIdx)"
      />
    </div>
  </div>
</template>