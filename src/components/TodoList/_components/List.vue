<script setup>
let id = 0;
const props = defineProps({
  todos: Array,
});
console.log("props", props.todos);
const removeTodo = (todo) => {
  todos.value = todos.value.filter((item) => item !== todo);
};
</script>

<template>
  <ul>
    <li class="pb" v-for="todo in todos" :key="todo.id">
      {{ todo.text }}
      <button @click="removeTodo(todo)">Remove</button>
    </li>
  </ul>
</template>

<style scoped>
ul {
  padding: 24px;
  list-style: none;
  display: flex;
  flex-direction: column;
}
.pb {
  padding-bottom: 10px;
}
ul > li {
  display: flex;
  align-items: center;
  font-weight: 500;
  justify-content: space-between;
  font-size: 16px;
  color: #000;
}
button {
  display: flex;
  background-color: #41b883;
  border: 0;
  font-weight: 500;
  padding: 9px;
}
button:hover {
  opacity: 0.6;
  cursor: pointer;
}
</style>