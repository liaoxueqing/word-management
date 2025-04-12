<template>
  <div class="poetry-list-management">
    <h1>{{ poetryList.length }}</h1>
  </div>
</template>

<script>
export default {
  name: 'PoetryManagement',
  props: {
    poetryList: Array
  }
}
</script>

<style scoped>
</style>
