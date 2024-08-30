<script setup lang="ts">
defineProps<{ text: string }>();
</script>

<template>
  <div v-if="text" className="error-display">{{ text }}</div>
</template>

<style scoped>
.error-display {
  font-family: 'inter';
  color: red;
}
</style>
