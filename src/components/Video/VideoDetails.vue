<script setup>
  //define properties
  const props = defineProps(['description', 'username']);
</script>

<template>
  <div>
    <h3>{{ username }}</h3>
    <p>{{ description }}</p>
  </div>
</template>

<style scoped>

</style>
