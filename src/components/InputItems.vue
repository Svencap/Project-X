<template>
  <div>
    <v-text-field v-for="input of inputs" :key="input" :label="input" />
  </div>
</template>

<script setup>
const inputs = [1, 2, 3, 4];
</script>