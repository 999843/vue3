<script setup>
import { ref } from "vue";
// const inputValue = ref("");
const propps = defineProps({ inputValue: String });

const handClick = () => {};
</script>

<template>
  <div class="search">
    <div>
      <input type="text" />
      <div class="addBtn" @click="handClick">Add Task</div>
    </div>
  </div>
</template>

<style scoped="scss">
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

input {
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