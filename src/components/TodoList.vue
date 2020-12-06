<template>
  <div>
    <h1 v-show="todoList.length === 0">List is empty</h1>
    <ul v-show="todoList.length !== 0">
      <TodoItem
        v-for="todoItem of todoList"
        :key="todoItem.id"
        v-bind:todoItem="todoItem"
        v-on:remove-item="removeTodoItem"
        v-on:edit-item="editTodoItem"
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
  methods: {
    editTodoItem(id) {
      this.$emit("edit-item", id);
    },
    removeTodoItem(id) {
      this.$emit("remove-item", id);
    },
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
