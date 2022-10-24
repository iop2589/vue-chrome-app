<template>
  <div>
    <clock-time></clock-time>
    <greeting-login></greeting-login>
    <weather-info></weather-info>
  </div>
</template>

<script>
import GreetingLogin from "./components/GreetingLogin.vue";
import ClockTime from "./components/ClockTime.vue";
import WeatherInfo from "./components/WeatherInfo.vue";
export default {
  components: {
    "greeting-login": GreetingLogin,
    "clock-time": ClockTime,
    "weather-info": WeatherInfo
  }
}
</script>

<style>

</style>