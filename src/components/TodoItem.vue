<template>
  <li>
    <span :class="{ done: checked }"
      ><input
        type="checkbox"
        v-model="checked"
        :checked="checked"
        v-on:change="changeCompletedField(todoItem.id)"
      />{{ todoItem.title }}</span
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
  methods: {
    changeCompletedField(id) {
      localStorage.setItem(
        "todoList",
        JSON.stringify(
          JSON.parse(localStorage.getItem("todoList")).map((todoItem) => {
            if (todoItem.id === id) {
              todoItem.completed = this.checked;
            }
            return todoItem;
          })
        )
      );
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
  padding: 2px 10px;
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
