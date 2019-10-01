<template>
<div id="app">
    <h1>VueJS: Weather</h1>

    <weather></weather>

</div>

</template>

<script>


export default {
  name: 'app',
  data() {
    return {
      city: "",
      submitted: false,
      weather: {}
    };
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
