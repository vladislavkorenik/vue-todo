<template>
  <div class="todo-app">
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
  </div>
</template>

<script>
import TodoList from "@/components/TodoList";
import EditModal from "@/components/EditModal";
import AddItem from "@/components/AddItem";

export default {
  name: "App",
  data() {
    return {
      filter: "completed",
      showModal: false,
      currentItemName: "",
      editItemId: "",
      todoList: JSON.parse(localStorage.getItem("todoList")) || [],
    };
  },
  mounted() {
    if (!JSON.parse(localStorage.getItem("todoList"))?.length) {
      fetch("https://jsonplaceholder.typicode.com/todos?_limit=10")
        .then((response) => response.json())
        .then((json) => {
          localStorage.setItem("todoList", JSON.stringify(json));
          this.todoList = json;
        });
    }
  },
  components: {
    TodoList,
    EditModal,
    AddItem,
  },
  methods: {
    addItem(itemTitle) {
      let todoList = JSON.parse(localStorage.getItem("todoList"));

      todoList = [
        { completed: false, id: Math.random(), title: itemTitle },
        ...this.todoList,
      ];

      this.todoList = todoList;
      localStorage.setItem("todoList", JSON.stringify(todoList));
    },
    searchItem(itemTitle) {
      if (!itemTitle.trim()) {
        this.todoList = JSON.parse(localStorage.getItem("todoList"));
      } else {
        this.todoList = this.todoList.filter(
          (todoItem) => todoItem.title.indexOf(itemTitle.trim()) !== -1
        );
      }
    },
    setItemName(itemName) {
      let todoList = JSON.parse(localStorage.getItem("todoList"));

      todoList = todoList.map((todoItem) => {
        if (todoItem.id === this.editItemId) {
          todoItem.title = itemName;
        }
        return todoItem;
      });

      this.todoList = todoList;
      localStorage.setItem("todoList", JSON.stringify(todoList));
    },
    hideModal() {
      this.showModal = false;
      this.$emit("modal-state", this.showModal);
    },
    editTodoItem(id) {
      this.todoList.forEach((todoItem) => {
        if (todoItem.id === id) {
          this.currentItemName = todoItem.title;
          this.editItemId = todoItem.id;
        }
      });

      this.showModal = true;
      this.$emit("modal-state", this.showModal);
    },
    removeTodoItem(id) {
      let todoList = JSON.parse(localStorage.getItem("todoList"));

      todoList = todoList.filter((todoItem) => todoItem.id !== id);

      this.todoList = todoList;
      localStorage.setItem("todoList", JSON.stringify(todoList));
    },
  },
};
</script>
