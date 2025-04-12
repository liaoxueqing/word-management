<template>
  <div class="words-management">
    <h1>{{ words.length }}</h1>
  </div>
</template>

<script>
export default {
  name: 'WordManagement',
  props: {
    words: Array
  }
}
</script>

<style scoped>
</style>
