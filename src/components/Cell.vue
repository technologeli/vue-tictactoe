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
  <button class="h-40 w-40 bg-slate-500" type="button" @click="$emit('change')">
    <X v-if="value === 1" />
    <O v-if="value === 2" />
  </button>
</template>