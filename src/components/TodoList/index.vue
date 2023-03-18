<script setup>
import { ref, computed } from "vue";
import List from "./_components/List.vue";
import Search from "./_components/Search.vue";
let id = 0;

const newTodo = ref("");
const hideCompleted = ref(false);
const todos = ref([
  { id: id++, text: "Learn HTML" },
  { id: id++, text: "Learn JavaScript" },
  { id: id++, text: "Learn Vue" },
]);

const filteredTodos = computed(() => {
  return hideCompleted.value ? todos.value.filter((t) => !t.done) : todos.value;
});

const addTodo = () => {
  todos.value.push({ id: id++, text: newTodo.value });
  newTodo.value = "";
};

const removeTodo = (todo) => {
  todos.value = todos.value.filter((t) => t !== todo);
};
</script>

<template>
  <section>
    <!-- <Search :inputValue="inputValue" />
    <List :todos="todos" /> -->
    <form class="search" @submit.prevent="addTodo">
      <div>
        <input v-model="newTodo" />
        <button class="addBtn">Add Todo</button>
      </div>
    </form>
    <ul>
      <li v-for="todo in filteredTodos" :key="todo.id">
        <div>
          <input type="checkbox" v-model="todo.done" />
          <span :class="{ done: todo.done }">{{ todo.text }}</span>
        </div>
        <button @click="removeTodo(todo)">Remove</button>
      </li>
    </ul>
    <div class="button">
      <button @click="hideCompleted = !hideCompleted">
        {{ hideCompleted ? "Show all" : "Hide completed" }}
      </button>
    </div>
  </section>
</template>

<style scoped>
section {
  max-width: 500px;
  min-height: 400px;
  margin-top: 40px;
  margin: 0 auto;
  background-color: #b9e7f3;
}
ul {
  padding: 24px;
  list-style: none;
  display: flex;
  gap: 20px;
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
ul > li > div {
  display: flex;
  gap: 6px;
}

.button {
  display: flex;
  justify-content: center;
  margin-top: 50px;
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

.search {
  background-color: #fff;
  padding-bottom: 12px;
  padding-top: 24px;
}
.search > div {
  display: flex;
  border-radius: 4px;
  overflow: hidden;
}

.search input {
  flex: 4;
  padding: 10px;
  outline-style: none;
  font-size: 20px;
  border: 1px solid rgb(228, 228, 228);
  border-top-left-radius: 4px;
  border-bottom-left-radius: 4px;
}
input:focus {
  border: 1px solid rgb(191, 215, 241);
}

.addBtn {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 16px;
  font-weight: 500;
  padding: 4px;
  background-color: #41b883;
}
.addBtn:hover {
  color: white;
  cursor: pointer;
  background-color: #34495e;
}
</style>