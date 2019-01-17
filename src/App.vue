<template>
  <div id="app">
    <div class="title">FCC Calculator App</div>
    <Calculator/>
  </div>
</template>

<script>
import Calculator from "./components/Calculator.vue";

export default {
  name: "app",
  components: {
    Calculator
  }
};
</script>

<style>
body {
  padding: 0;
  margin: 0;
}

#app {
  height: 100vh;
  width: 100vw;
  display: grid;

  justify-content: center;
  text-align: center;
}

.title {
  font-size: 4em;
  text-shadow: 1px 2px 9px black;
  margin-top: 50px;
}
</style>
