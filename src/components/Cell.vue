<script setup lang="ts">
import X from './X.vue';
import O from './O.vue';
const props = defineProps<{
  value: number,
  row: number,
  col: number,
}>();

const events = defineEmits(['change']);

</script>

<template>
  <button class="h-20 w-20 sm:h-40 sm:w-40 bg-slate-500" type="button" @click="$emit('change')">
    <X class="animate-fade-in" v-if="value === 1" />
    <O class="animate-fade-in" v-if="value === 2" />
  </button>
</template>