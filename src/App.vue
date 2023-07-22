<template>
  <div id="app">
    <h1>Calculadora</h1>
    <Calculadora />
  </div>
</template>

<script>
import Calculadora from './components/Calculadora.vue'

export default {
  name: 'App',
  components: {
    Calculadora
  }
}
</script>

<style>
@font-face {
  font-family: "RobotoMono";
  src: url("./fonts/RobotoMono-Thin.ttf");
}
* {
  font-family: "RobotoMono", monospace;
}
body {
  margin: 0;
}
#app {
  display: flex;
  flex-direction: column;
  height: 100vh;
  justify-content: center;
  align-items: center;
  text-align: center;
  color: white;
  background-color: rgb(39, 39, 39);
}

</style>
