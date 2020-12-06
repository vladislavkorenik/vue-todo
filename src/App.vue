<template>
  <div v-show="showModal" class="modal-background__div"></div>
  <img alt="Vue logo" src="./assets/logo.png" />
  <AddItem @add-item="addItem" @search-item="searchItem" />
  <TodoList
    :todoList="todoList"
    @edit-item="editTodoItem"
    @remove-item="removeTodoItem"
  />
  <EditModal
    :currentItemName="currentItemName"
    v-show="showModal"
    @hide-modal="hideModal"
    @set-item-name="setItemName"
  />
</template>

<script>
import TodoList from "@/components/TodoList";
import EditModal from "@/components/EditModal";
import AddItem from "@/components/AddItem";

export default {
  name: "App",
  data() {
    return {
      showModal: false,
      currentItemName: "",
      editItemId: "",
      todoList: [],
    };
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=10")
      .then((response) => response.json())
      .then((json) => {
        this.todoList = json;
      });
  },
  components: {
    TodoList,
    EditModal,
    AddItem,
  },
  methods: {
    addItem(itemTitle) {
      this.todoList = [
        { completed: false, id: Math.random(), title: itemTitle },
        ...this.todoList,
      ];
    },
    searchItem(itemTitle) {
      console.log(itemTitle, "search");
    },
    setItemName(itemName) {
      this.todoList = this.todoList.map((todoItem) => {
        if (todoItem.id === this.editItemId) {
          todoItem.title = itemName;
        }
        return todoItem;
      });
    },
    hideModal() {
      this.showModal = false;
    },
    editTodoItem(id) {
      this.todoList.forEach((todoItem) => {
        if (todoItem.id === id) {
          this.currentItemName = todoItem.title;
          this.editItemId = todoItem.id;
        }
      });
      this.showModal = true;
    },
    removeTodoItem(id) {
      this.todoList = this.todoList.filter((todoItem) => todoItem.id !== id);
    },
  },
};
</script>

<style>
button {
  border: none;
  outline: none;
  color: #2c3e50;
  font-weight: bolder;
}
button,
input {
  cursor: pointer;
}
body {
  padding: 0;
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
<style scoped>
.modal-background__div {
  content: "";
  position: fixed;
  width: 100%;
  height: 100%;
  background: gray;
  opacity: 0.5;
}
img {
  margin-top: 60px;
}
</style>
