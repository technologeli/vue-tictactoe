<script setup lang="ts">
import Board from './components/Board.vue';
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import { ref } from 'vue';
import Player from './components/Player.vue';

const handleWinner = (winner: number) => {
  if (winner === 1) player1Wins.value++;
  else player2Wins.value++;
}

const handlePlayerName = (playerName: string, player: number) => {
  if (playerName !== '') {
    if (player === 1) player1Name.value = playerName;
    else player2Name.value = playerName;
  }
  else {
    if (player === 1) player1Name.value = 'Player X';
    else player2Name.value = 'Player O';
  }
}

const player1Name = ref('Player X');
const player1Wins = ref(0);

const player2Name = ref('Player O');
const player2Wins = ref(0);
</script>

<template>
  <nav class="block px-2 py-1 bg-slate-500">
    <h1 class="text-center text-6xl font-bold text-slate-900">Tic Tac Toe</h1>
  </nav>
  <main class="pt-4 mx-auto">
    <Player class="grow" @change:name="handlePlayerName" :player="1" :wins="player1Wins" />
    <div class="flex items-center justify-center">
      <Board @change:winner="handleWinner" :player1-name="player1Name" :player2-name="player2Name" />
    </div>
    <Player class="grow" @change:name="handlePlayerName" :player="2" :wins="player2Wins" />
  </main>
</template>

<style>
</style>
