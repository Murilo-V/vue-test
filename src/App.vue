<template>
  <div
    class="
      vh-100
      container-fluid
      d-flex
      justify-content-center
      align-items-center
    "
  >
    <Main />
  </div>
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
  box-sizing: border-box;
  font-family: "Open Sans", sans-serif;
}

html,
body {
  background-color: #ffe766;
}

h1 {
  color: #483698;
}

h1,
button {
  font-family: "Comfortaa", cursive;
}

input,
select {
  padding: 0.25rem 0.25rem 0.25rem 1.2rem;
  border-radius: 0.3rem;
  border: 2px solid #403c94;
  background-color: #fff;
  outline: none;
  width: 100%;
}

.invalidInput {
  border: 2px solid #dc3545;
}

.invalidText {
  color: #dc3545;
}
</style>
