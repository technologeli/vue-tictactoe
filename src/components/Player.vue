<script setup lang="ts">
import { ref } from 'vue';
import Tally from './Tally.vue';

const playerName = ref('');

defineProps<{
  player: number;
  wins: number;
}>();

defineEmits<{
  (e: 'change:name', playerName: string, player: number): void
}>();

const handleChange = ($event: Event, $emit: (e: 'change:name', playerName: string, player: number) => void, player: number) => {
  playerName.value = (<HTMLInputElement>$event.target).value;
  $emit('change:name', playerName.value, player);
}

</script>

<template>
  <div class="mx-auto px-2 py-2 flex flex-col space-y-2 max-w-2xl">
    <h2 class="text-center text-3xl font-bold text-slate-500">Player {{ player === 1 ? 'X' : 'O' }}</h2>
    <input
      class="py-1 grow bg-slate-800 text-slate-50 text-3xl text-center rounded-full placeholder:text-slate-700"
      type="text"
      placeholder="Name"
      :value="playerName"
      maxlength="20"
      @input="handleChange($event, $emit, player)"
    />
    <div class="p-1 flex flex-wrap space-x-4">
      <Tally v-for="n in Math.floor(wins / 5)" :key="n" :value="5" />
      <Tally :value="wins % 5" />
    </div>
  </div>
</template>