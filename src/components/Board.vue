<script setup lang="ts">
import Cell from './Cell.vue';
import { reactive, ref } from 'vue';

const createBoard = () => reactive([
  [0, 0, 0],
  [0, 0, 0],
  [0, 0, 0],
])

let board: number[][] = reactive([
  [0, 0, 0],
  [0, 0, 0],
  [0, 0, 0],
]);

let turn = 1; // player 1 (X) goes first
const winner = ref<number | undefined>();

const reset = () => {
  for (let i = 0; i < board.length; i++) {
    for (let j = 0; j < board[i].length; j++) {
      board[i][j] = 0;
    }
  }
  turn = 1;
  winner.value = undefined;
}

const play = (
  rowIdx: number,
  colIdx: number,
  $emit: (event: "change:winner", value: number) => void
) => {
  if (!winner.value && board[rowIdx][colIdx] === 0) {
    board[rowIdx][colIdx] = turn;

    if (all(getDiagonal(true), turn) || all(getDiagonal(false), turn)) {
      winner.value = turn;
      $emit('change:winner', winner.value);
      return;
    }

    for (let i = 0; i < board.length; i++) {
      if (all(getRow(i), turn) || all(getCol(i), turn)) {
        winner.value = turn;
        $emit('change:winner', winner.value);
        return;
      }
    }

    changePlayer();
  }
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

defineProps<{ player1Name: string; player2Name: string; }>();

defineEmits<{
  (e: 'change:winner', value: number): void
}>();

</script>

<template>
  <div
    class="bg-slate-600 rounded flex flex-col space-y-2 p-2 transition"
    :class="{ 'brightness-50': winner }"
  >
    <div v-for="(row, rowIdx) in board" class="flex space-x-2">
      <Cell
        v-for="(col, colIdx) in row"
        :value="col"
        :row="rowIdx"
        :col="colIdx"
        :key="`${rowIdx} ${colIdx}`"
        @change="play(rowIdx, colIdx, $emit)"
      />
    </div>
  </div>
  <div class="absolute flex flex-col space-y-4" v-if="winner">
    <div
      class="px-4 py-4 bg-slate-300 rounded-full font-semibold text-slate-900 text-center text-3xl shadow-4xl shadow-slate-700/40 animate-drop-in"
    >{{ `${winner === 1 ? player1Name : player2Name} wins!` }}</div>
    <button
      @click="reset()"
      class="px-4 py-4 bg-slate-300 hover:bg-slate-400 active:bg-slate-500 transition rounded-full font-semibold text-slate-900 text-center text-3xl shadow-4xl shadow-slate-700/40 animate-drop-in"
    >Reset Board</button>
  </div>
</template>