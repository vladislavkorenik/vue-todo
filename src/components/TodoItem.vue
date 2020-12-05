<template>
  <li>
    <span
      ><input type="checkbox" />{{ todoItem.title }}
      <button>&times;</button></span
    >
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
};
</script>

<style scoped>
span {
  width: 300px;
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
}
button,
input {
  cursor: pointer;
}
button {
  outline: none;
  background: crimson;
  border: none;
  width: 20px;
  height: 20px;
  border-radius: 50%;
}
button:hover {
  color: white;
  background: rgb(94, 16, 32);
}
</style>
