<script setup lang="ts">
import { ref } from 'vue';
import NameDisplay from './NameDisplay.vue';
import { fetchGenderByName } from '../api/fetchGenderByName';
import ErrorDisplay from './ErrorDisplay.vue';

const person = ref({ name: '', gender: '' });
const error = ref('');

// defineProps<{ msg: string }>();
async function handleSubmit() {
  if (error.value) {
    return;
  }

  const genderFetch = await fetchGenderByName(person.value.name);
  if (!genderFetch.status) {
    error.value = 'Failed Fetch!';
    return;
  }

  person.value = { ...person.value, gender: genderFetch.gender };
}

function handleChange(e: Event) {
  const target = e.target as HTMLInputElement;
  const newName = target.value;
  let newError = '';

  if (newName.length === 0) {
    error.value = newError;
    person.value = { name: '', gender: '' };
    return;
  }

  if (newName.length > 20) {
    newError = 'No more than 20 characters!';
  } else if (!/^[A-Za-z\s]+$/.test(newName)) {
    newError = 'Use only latin alphabet!';
  }

  error.value = newError;
  person.value = { name: newName, gender: '' };
}
</script>

<template>
  <form @submit.prevent="handleSubmit">
    <div className="name-input">
      <input
        type="text"
        name="name"
        v-model="person.name"
        placeholder="Enter name..."
        @input="handleChange"
      />
      <button type="submit">Genderize!</button>
    </div>
    <ErrorDisplay :text="error" />
    <div className="name-for-genderize">
      <NameDisplay :name="person.name" :gender="person.gender" />
    </div>
  </form>
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  gap: 20px;
  max-width: 100%;
}

.name-input {
  display: flex;
  justify-content: space-between;
  gap: 10px;
}
input {
  padding: 6px 8px;
  border: 1px solid var(--orange);
  border-radius: 10px;
  font-size: 16px;
  font-family: 'Inter';
  font-weight: normal;
  width: 100%;
}
button {
  cursor: pointer;
  font-family: 'Inter';
  color: white;
  padding: 8px;
  border-radius: 10px;
  border: 1px solid var(--orange);
  background-color: var(--orange);
}

.disabled {
  border: 1px solid var(--grey);
  background-color: var(--grey);
}
</style>
