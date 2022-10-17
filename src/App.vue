<template>
  <div id="app">
    <WeatherDash v-if="currentWeather" :currentWeather="currentWeather"></WeatherDash>
    <div v-else>No Weather</div>
  </div>
</template>

<script>
import axios from 'axios'
import WeatherDash from './components/WeatherDash.vue'
export default {
  name: 'App',
  components: {
    WeatherDash
  },
  data: () => ({
    dailyWeather:[],
    currentWeather:null
  }),
  mounted: function(){
    navigator.geolocation.getCurrentPosition(async (position) => {
      console.log(position.coords)
      await this.getCurrentWeather(position.coords)
    })
  },
  methods :{
    async getCurrentWeather(coords){
      const res = await axios.get(`https://api.openweathermap.org/data/2.5/onecall?lat=${coords.latitude}&lon=${coords.longitude}&units=imperial&appid=0251ad61db2d6a9d1a8305a0baa60f53`)
      this.currentWeather = res.data.current
    }
  }
}
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