<script setup>
import { ref } from "vue";
const isDark = ref(false);

function dark() {
  isDark.value = !isDark.value;
}
</script>

<template>
  <footer :class="{ dark: isDark }">
    <h2>this is the footerr</h2>
  </footer>

  <button @click="dark">toogle footer style</button>
</template>

<style>
.footer {
  padding: 3px;
  background-color: #eee;
  transition: 0.2s;
}

.dark {
  background-color: #222;
  color: white;
}
</style>
