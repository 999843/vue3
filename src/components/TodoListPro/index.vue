<script setup>
import Item from "../TodoListPro/Item/index.vue";
import { computed, ref, watch, watchEffect } from "vue";
const gridData = [
  { name: "Chuck Norris", id: "1" },
  { name: "Bruce Lee", id: "2" },
  { name: "Jackie Chan", id: "4" },
  { name: "Jet Li", id: "f2" },
];

const list = ref(JSON.parse(window.localStorage.getItem("list")) || gridData);

const uid = ref(4);
const searchValue = ref("");
const addValue = ref("");

const randomUid = () => {
  const charStr = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz";
  const randomChar = charStr[Math.floor(Math.random() * charStr.length)];
  return `${randomChar}${Math.floor(Math.random() * 1000000000)}`;
};
const handleClick = () => {
  const number = Math.floor(Math.random() * 1000000000);
  console.log("number", number);
  if (addValue.value.trim() !== "") {
    list.value.push({
      name: addValue.value,
      id: randomUid(),
    });
  }
  addValue.value = "";
};

const filterData = computed(() => {
  if (searchValue) {
    return list.value.filter((item) =>
      item.name.toLocaleLowerCase().startsWith(searchValue.value)
    );
  }
  return list.value;
});

const handleRemove = (todo) => {
  list.value = list.value.filter((item) => item.id !== todo.id);
};

watchEffect(() => {
  window.localStorage.setItem("list", JSON.stringify(list.value));
});
</script>
<template >
  <div class="main">
    <div class="box">
      <div class="search">
        <input v-model="searchValue" placeholder="search" />
      </div>

      <TransitionGroup tag="ul" name="fade" class="container">
        <Item
          v-for="item in filterData"
          :key="item.id"
          :todo="item"
          :handleRemove="handleRemove"
        />
        <li key="button" class="button">
          <input v-model="addValue" placeholder="Add new todo" />
          <button @click="handleClick">Add</button>
        </li>
      </TransitionGroup>
    </div>
  </div>
</template>

<style lang="css" scoped>
.main {
  display: flex;
  align-items: center;
  min-height: 1000px;
  background: #f5f5f5;
}
.search {
  padding-bottom: 10px;
  display: flex;
  align-items: center;
  gap: 3px;
}
input {
  width: 100%;
  height: 36px;
  outline: none;
}
.container {
  position: relative;
  list-style-type: none;
}
.box {
  width: fit-content;
  margin: 0 auto;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.05);
  overflow: hidden;
}
.button {
  display: flex;
}
ul {
  background-color: white;
  padding: 20px;
  width: 800px;
  margin: 0 auto;
  list-style: none;
}
/* 1. 声明过渡效果 */
.fade-move,
.fade-enter-active,
.fade-leave-active {
  transition: all 0.5s ease;
}

/* 2. 声明进入和离开的状态 */
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: scaleY(0.01) translate(30px, 0);
}

/* 3. 确保离开的项目被移除出了布局流
      以便正确地计算移动时的动画效果。 */
.fade-leave-active {
  position: absolute;
}
</style>