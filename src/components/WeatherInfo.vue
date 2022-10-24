<template>
    <div>  
        <div v-if="isError">
            <span>사용자 위치 정보를 찾을 수 없습니다. 날씨 정보를 제공하지 않습니다.</span>
        </div>
        <div v-else-if="!isLoading" id="weather" class="weather font-color">
            <p>{{ cityName }}</p>
            <p>{{ weather }} / {{ tempo }}</p>
        </div>
        <div class="weather font-color" v-else>
            Loading...
        </div>
    </div>
</template>

<script>
import axios from "axios";

const apiUrl = "https://api.openweathermap.org/data/2.5/weather?";
const API_KEY = "4124fcd17ceef2d21cb97b7c60988f3a";

export default {
    data: function () {
        return {
            weather: "",
            tempo: "",
            cityName: "",
            isLoading: true,
            isError: false
        }
    },
    mounted: function () {
        navigator.geolocation.getCurrentPosition(this.onGeoOk, this.onGeoError);
    },
    methods: {
        onGeoOk: async function (position) {
            const lat = position.coords.latitude;
            const lon = position.coords.longitude;

            const apiCallUrl = `${apiUrl}lat=${lat}&lon=${lon}&appid=${API_KEY}&units=metric`;

            let response = await axios.get(apiCallUrl);
            let data = response.data;

            this.weather = data.weather[0].main;
            this.tempo = data.main.temp;
            this.cityName = data.name;
            this.isLoading = false;
        },
        onGeoError: function () {
            alert("사용자 위치 정보를 찾을 수 없습니다. 날씨 정보를 제공하지 않습니다.");
            this.isError = true;
            this.isLoading = false;
        }
    }
}
</script>

<style>

</style>