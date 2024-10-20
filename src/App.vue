<script setup>
import Example from "./components/Example.vue";
import TodoList from "./components/TodoList/index.vue";
import TodoListPro from "./components/TodoListPro/index.vue";
</script>

<template>
  <header>
    <img
      alt="Vue logo"
      class="logo"
      src="./assets/logo.svg"
      width="125"
      height="125"
    />
  </header>

  <main>
    <TodoList />
    <TodoListPro />
    <!-- <Example /> -->
  </main>
</template>

<style scoped>
header {
  display: flex;
  justify-content: center;
}
</style>
