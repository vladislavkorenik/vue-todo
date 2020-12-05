<template>
  <div>
    <ul>
      <TodoItem
        v-for="todoItem of todoList"
        :key="todoItem.id"
        v-bind:todoItem="todoItem"
      />
    </ul>
  </div>
</template>

<script>
import TodoItem from "@/components/TodoItem";
export default {
  props: ["todoList"],
  components: {
    TodoItem,
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
