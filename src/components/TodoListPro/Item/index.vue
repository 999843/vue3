
<script setup>
const { todo, handleRemove } = defineProps({
  handleRemove: Function,
  todo: {
    name: String,
    id: Number,
  },
});

const onClick = (todo) => {
  handleRemove(todo);
};
</script>

<template>
  <li>
    <div class="box">
      <p>{{ todo.name }}</p>
      <button type="button" @click="onClick(todo)">remove</button>
    </div>
  </li>
</template>


<style lang="css" scoped>
.box {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}
</style>