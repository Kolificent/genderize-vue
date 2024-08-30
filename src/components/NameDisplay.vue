<script setup lang="ts">
import BlinkingCursor from './BlinkingCursor.vue';

defineProps<{ name: string; gender: string | null }>();
</script>

<template>
  <div class="name-for-genderize">
    <BlinkingCursor v-if="!name" />
    <span v-else-if="gender"> {{ name }} is {{ gender }} </span>
    <span v-else>
      {{ name }}
      <BlinkingCursor /> is...
    </span>
  </div>
</template>

<style scoped>
.name-for-genderize {
  font-family: 'inter';
  font-weight: bold;
  font-size: 30px;
}
</style>
