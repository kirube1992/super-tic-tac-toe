<script setup>
import { ref, computed } from "vue";

const firstName = ref("");
const lastName = ref("");

const fullName = computed(() => {
  if (!firstName.value && !lastName.value) return "";
  return `${firstName.value} ${lastName.value}`;
});
</script>
<template>
  <input v-model="firstName" type="text" placeholder="firstName" />
  <input v-model="lastName" type="text" placeholder="lastNmae" />

  <h2>fullName {{ fullName }}</h2>
</template>

<style>
.input {
  margin: 0.5rem;
  padding: 0.5rem;
}
</style>
