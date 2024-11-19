<script setup>
defineProps({
  xCoord: Number,
  yCoord: Number
});
</script>

<template>
  <p>
    Координаты:
    X: <span>{{ xCoord }}</span>
    Y: <span>{{ yCoord }}</span>
  </p>
</template>

<style scoped>

</style>