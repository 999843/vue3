<script setup>
const props = defineProps({
  searchValue: string,
});
</script>

<template >
  <form action="">
    <input type="text" v-model="searchValue" placeholder="Add new todo" />
  </form>
</template>

<style lang="scsss">
</style>