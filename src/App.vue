<template>
<div id="app">
    <h1>VueJS: Weather</h1>
    <input type="text" placeholder="City" v-model="city">
    <form @submit.prevent="getWeather">
      <input type="text" placeholder="City" v-model="city">
    </form>
    <weather></weather>
         <div v-if="submitted">
          <h2>{{ weather.name }} Weather</h2>
          <div class="description">{{ weather.description }}</div>
          <div class="temp">It's currently {{ weather.temp }}° F.</div>
          <div class="highlow">High: {{ weather.high }}° F. Low: {{ weather.low }}° F.</div>
      </div>

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
  methods: {
    getWeather(){
      this.weather = {}
      this.submitted = false
      fetch(
        'http://api.openweathermap.org/data/2.5/find?q=${
          this.city
        }&units=metric&appid=6b3705bb90e87433d0711ed38d1e6062'
      )
       .then(response => response.json())
        .then(response => {
          let data = response.list[0];
          this.submitted = true;
          this.weather.name = data.name;
          this.weather.description = data.weather[0].main;
          this.weather.temp = Math.round(data.main.temp);
          this.weather.high = Math.round(data.main.temp_max);
          this.weather.low = Math.round(data.main.temp_min);
        })
        .catch(error => console.log(error));
      this.city = "";
    }
    }
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
