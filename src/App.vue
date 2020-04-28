<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <txtComponent msg="Vue Component" usrData="English, Tamil, Japanese" />
  </div>
</template>

<script>
import txtComponent from "./components/txtComponent";

export default {
  name: "App",
  components: {
    txtComponent
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
