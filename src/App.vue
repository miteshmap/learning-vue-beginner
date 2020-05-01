<template>
  <div id="app">
    <img width="25%" src="./assets/logo.png">
    <product></product>
  </div>
</template>

<script>
import product from "./components/product";

export default {
  name: "App",
  components: {
    product
  }
};
</script>

<style>
body {
  background: black;
  color: white;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
</style>
