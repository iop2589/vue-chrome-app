<template>
  <div>
    <clock-time></clock-time>
    <greeting-login></greeting-login>
    <weather-info></weather-info>
    <to-do></to-do>
    <today-quote></today-quote>
  </div>
</template>

<script>
import GreetingLogin from "./components/GreetingLogin.vue";
import ClockTime from "./components/ClockTime.vue";
import WeatherInfo from "./components/WeatherInfo.vue";
import ToDo from "./components/ToDo.vue";
import TodaysQuote from "./components/TodayQuotes.vue";
export default {
  computed: {
      img: function(){
          const images = ["1.jpg", "2.jpg", "3.jpg"]
          const choosenImage = images[Math.floor(Math.random() * images.length)];
          return require(`@/assets/img/${choosenImage}`);
    }
  },
  mounted: function () {
    this.setBackgroundImage();
  },
  components: {
    "greeting-login": GreetingLogin,
    "clock-time": ClockTime,
    "weather-info": WeatherInfo,
    "to-do": ToDo,
    "today-quote": TodaysQuote
  },
  methods: {
    setBackgroundImage: function () {
      document.body.style.backgroundImage = `url(${this.img})`;
    }
  }
}
</script>

<style>
  @import "../src/assets/css/style.css";
</style>