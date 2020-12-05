<template>
  <div class="edit-modal__div">
    <h1>Edit item name</h1>
    <input :class="{ errorInput: errorAlert }" v-model="title" />
    <div class="buttons">
      <button v-on:click="submitButtonHandler" class="submit-button">OK</button>
      <button v-on:click="$emit('hide-modal')" class="cancel-button">
        Cancel
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["currentItemName"],
  data() {
    return {
      title: "",
      errorAlert: false,
    };
  },
  watch: {
    currentItemName() {
      this.title = this.currentItemName;
      this.errorAlert = false;
    },
  },
  methods: {
    submitButtonHandler() {
      if (this.title.trim()) {
        this.$emit("set-item-name", this.title);
        this.$emit("hide-modal");
      } else this.errorAlert = true;
    },
  },
};
</script>

<style scoped>
.errorInput {
  border: 2px solid crimson;
}
.buttons button {
  border: 1px solid #2d6f52;
  font-weight: bolder;
  color: #35495e;
}
.submit-button {
  background: #41b883;
  margin-right: 10px;
}
.cancel-button {
  background: crimson;
  margin-right: 10px;
}
.submit-button:hover {
  background: #113d2a;
  color: #ffffff;
}
.cancel-button:hover {
  color: white;
  background: rgb(94, 16, 32);
}
h1 {
  margin: 10px 0;
}
input {
  outline: none;
  border-radius: 0px;
  border: 2px solid #41b883;
  margin-bottom: 10px;
}
.edit-modal__div {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  max-width: 350px;
  width: 100%;
  padding: 25px 10px;
  background: white;
}
</style>
