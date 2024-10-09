<template>
    <div>
        <h1>Weather App</h1>
        <input v-model="city" @keyup.enter="getWeather" placeholder="Enter city name" />
        <button @click="getWeather">Get Weather</button>
        <div v-if="weather">
            <h3>Weather in {{ weather.name }}</h3>
            <p>Temperature: {{ weather.main.temp }}°F</p>
            <p>Humidity: {{ weather.main.humidity }}%</p>
            <p>Condition: {{ weather.weather[0].description }}</p>
        </div>
    </div>
</template>
<script>
import axios from 'axios'

export default {
    data() {
        return {
            city: '',
            weather: null,
        }
        
    },
    methods: {
        async getWeather() {
            if (this.city.trim()){
                try {
                    const apiKey = '9e9bf87681e2b908042ca1a8e0b10290';
                    const response = await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${apiKey}&units=imperial`);
                    this.weather = response.data;} 
                    catch (error) {
                    console.error('error fetching weather data', error);
                    }
                }
            }
        }
                
    }
</script>
<style scoped>
input{
    margin-right: 10px;
}</style>
