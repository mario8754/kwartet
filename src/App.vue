<template>
  <div id="app">
    <PlayField />
  </div>
</template>

<script>
import PlayField from "./components/PlayField.vue";

export default {
  name: "App",
  components: {
    PlayField,
  },
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
