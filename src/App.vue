<template>
  <div v-show="showModal" class="modal-background__div"></div>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/todo-app">Application</router-link>
  </div>
  <img alt="Vue logo" src="./assets/logo.png" />
  <router-view @modal-state="getModalState" />
</template>

<script>
export default {
  data() {
    return {
      showModal: false,
    };
  },
  methods: {
    getModalState(modalState) {
      this.showModal = modalState;
    },
  },
};
</script>

<style>
button {
  border: none;
  color: #2c3e50;
  font-weight: bolder;
}
button,
input,
select {
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
  outline: none;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
.modal-background__div {
  content: "";
  position: fixed;
  width: 100%;
  height: 100%;
  background: gray;
  opacity: 0.5;
}
</style>
