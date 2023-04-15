<template>
<article>
    <p id="temp"></p> 
</article>
</template>
    
<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const apiUrl = 'https://api.openweathermap.org/data/2.5/weather';
const apiKey = 'e4f5d4086edc70493ee3c27099fff3d2';
const city = ref('London');

function getTemperature() {
    axios.get(apiUrl, {
        params: {
            q: city.value,
            appid: apiKey,
            units: 'metric'
        }
    })
    .then(response => {
        const temperature = response.data.main.temp;
        console.log(`Current temperature in ${city.value}: ${temperature}°C`);
        document.getElementById('temp').innerHTML = temperature + '°C';
    })
    .catch(error => {
        console.log('Error:', error);
    });
}

onMounted(() => {
    getTemperature();
    setInterval(getTemperature, 3000);
});
</script>

<style scoped>
</style>