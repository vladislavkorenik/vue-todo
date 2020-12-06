<template>
  <div class="add-block">
    <input type="text" v-model="inputValue" />
    <button v-on:click="buttonHandler('add-item')">Add</button>
    <SearchItem @search-item-click="buttonHandler('search-item')" />
  </div>
</template>

<script>
import SearchItem from "@/components/SearchItem";
export default {
  data() {
    return {
      inputValue: "",
    };
  },
  components: {
    SearchItem,
  },
  methods: {
    buttonHandler(actionName) {
      if (!this.inputValue.trim() && actionName === "search-item") {
        this.$emit("search-item", this.inputValue);
      }
      if (this.inputValue.trim()) {
        actionName === "add-item"
          ? this.$emit("add-item", this.inputValue)
          : this.$emit("search-item", this.inputValue);
        this.addValue = "";
      }
    },
  },
};
</script>

<style scoped>
.add-block {
  margin-bottom: 10px;
}
button {
  background: none;
  border: 2px solid #41b883;
}
button:hover {
  border: 2px solid #113d2a;
}
</style>
