<template>
  <li>
    <span :class="{ done: checked }"
      ><input type="checkbox" v-model="checked" :checked="checked" />{{
        todoItem.title
      }}</span
    >
    <div>
      <button class="edit-button" v-on:click="$emit('edit-item', todoItem.id)">
        Edit
      </button>
      <button
        class="remove-button"
        v-on:click="$emit('remove-item', todoItem.id)"
      >
        &times;
      </button>
    </div>
  </li>
</template>

<script>
export default {
  props: {
    todoItem: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      checked: this.todoItem.completed || false,
    };
  },
};
</script>

<style scoped>
li {
  display: flex;
  margin-bottom: 10px;
}
.done {
  color: darkgray;
  text-decoration: line-through;
}
span {
  width: 300px;
  display: flex;
  justify-content: space-between;
  text-align: end;
}
.edit-button {
  margin: 0 10px;
  background: #41b883;
  color: #35495e;
  padding: 2px 10px;
  font-weight: bold;
}
.edit-button:hover {
  background: #113d2a;
  color: #ffffff;
}
.remove-button {
  background: crimson;
  width: 20px;
  height: 20px;
  border-radius: 50%;
}
.remove-button:hover {
  color: white;
  background: rgb(94, 16, 32);
}
@media screen and (max-width: 480px) {
  span {
    width: 200px;
  }
}
</style>
