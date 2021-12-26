<script setup lang="ts">
defineProps<{ value: number; }>();
</script>

<template>
  <div class="flex space-x-1">
    <div v-if="value >= 1" class="h-10 w-2 rounded-full bg-slate-500"></div>
    <div v-if="value >= 2" class="h-10 w-2 rounded-full bg-slate-500"></div>
    <div v-if="value >= 3" class="h-10 w-2 rounded-full bg-slate-500"></div>
    <div v-if="value >= 4" class="h-10 w-2 rounded-full bg-slate-500"></div>
    <div
      v-if="value >= 5"
      class="absolute translate-y-4 -translate-x-3.5 h-2 w-16 rounded-full bg-slate-500 -rotate-[20deg]"
    ></div>
  </div>
</template>