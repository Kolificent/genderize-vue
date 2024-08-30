<script setup lang="ts">
import NameForm from './components/NameForm.vue';
</script>

<template>
  <div class="app-container">
    <div className="logo">
      <h1>Genderize</h1>
      <h2>check the gender of a name</h2>
    </div>
    <NameForm />
  </div>
</template>

<style scoped>
h1 {
  font-family: 'inter';
  font-weight: bold;
}

h2 {
  font-family: 'inter';
  font-weight: normal;
  font-size: 16px;
}

.app-container {
  display: flex;
  max-width: 600px;
  background-color: white;
  border-radius: 10px;
  justify-content: center;
  flex-direction: column;
  padding: 20px;
  gap: 10px;
}
</style>
