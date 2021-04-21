<template>
  <div id="app">
    <cart-component></cart-component>
  </div>
</template>

<script>
import CartComponent from "./components/CartComponent";

export default {
  name: "App",
  components: {
    CartComponent,
  },
};
</script>

<style>
/* #app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
</style>
