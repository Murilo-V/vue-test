<template>
  <Main />
</template>

<script>
import Main from "./view/Main.vue";

export default {
  name: "App",
  components: {
    Main,
  },
};
</script>

<style>
*,
html,
body {
  margin: 0;
  padding: 0;
  border: 0;
  outline: 0;
  box-sizing: border-box;
  font-family: "Open Sans", sans-serif;
}

html,
body {
  background-color: #ffe766;
}

h1,
button {
  font-family: "Comfortaa", cursive;
}
</style>
