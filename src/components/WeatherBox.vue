<template>
<article>
    <div class="weather-box">
        <div id="temp">{{ temperature }}</div>
        <div class="color-size" id="weather">{{ weather }}</div>
        <div id="city-name">{{ city }}</div>
        <div class="color-size" id="date">{{ date }}</div>
        <div class="color-size" id="humidity"><i class="icon-tint"></i>&nbsp;{{ humidity }}</div>
        <div class="color-size" id="feeling"><i class="icon-smile"></i>&nbsp; Feels: {{ feelingTemperature }}</div>
    </div>
</article>
</template>
    
<script setup>
import { ref, onMounted, watch } from 'vue';
import { store } from '../store.js'
import axios from 'axios';

const apiUrl = 'https://api.openweathermap.org/data/2.5/weather';
const apiKey = 'e4f5d4086edc70493ee3c27099fff3d2';
let temperature = ref('');
let weather = ref('');
let city = ref(store.selectedLocation);
let date = ref('');
let humidity = ref('');
let feelingTemperature = ref('');
let alreadyRun = false;

function getWeatherData() {
    axios.get(apiUrl, {
        params: {
            q: store.selectedLocation,
            appid: apiKey,
            units: 'metric'
        }
    })
    .then(response => {
        temperature.value = Math.round(response.data.main.temp) + ' °C';
        feelingTemperature.value = Math.round(response.data.main.feels_like) + ' °C';
        humidity.value = response.data.main.humidity + '%';
        weather.value = response.data.weather[0].main;
        city.value = response.data.name;
        date.value = getCurrentDate();
        alreadyRun = false

        console.log(`Current temperature in ${city.value}: ${temperature.value}°C`);
    })
    .catch(error => {
        console.log('Error:', error);

        if (!alreadyRun) {
            console.log('hoi5555555')
            store.popup = true;
            alreadyRun = true;
        }
    });
}

function getCurrentDate() {
    const currentDate = new Date();
    const day = currentDate.getDate().toString().padStart(2, '0');
    const month = (currentDate.getMonth() + 1).toString().padStart(2, '0');
    const year = currentDate.getFullYear().toString();

    const formattedDate = `${day}-${month}-${year}`;
    return formattedDate;
}

onMounted(() => {
    getWeatherData();
    setInterval(getWeatherData, 5000);
});

watch(() => store.selectedLocation, async (newCity, oldCity) => {
    if (newCity !== oldCity) {
        getWeatherData();
    }
});
</script>

<style scoped>
article {
    display: flex;
    justify-content: center;
    padding: 100px 0;
}

.weather-box {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr 1fr 1fr;
    grid-template-areas:
        "city-name . date"
        ". temp ."
        "humidity weather feeling";
    padding: 30px;
    width: 600px;
    height: 325px;
    background-color: white;
    border-radius: 15px;
    box-shadow: 0 3px 10px #00000033;
}

i {
    font-size: 24px;
}

.color-size {
    font-size: 20px;
    color: #0062b3;
}

#temp {
    grid-area: temp;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 65px;
    font-weight: bold;
    color: #008cff;
}

#weather {
    grid-area: weather;
    display: flex;
    justify-content: center;
}

#city-name {
    grid-area: city-name;
    display: flex;
    justify-content: flex-start;
    font-size: 28px;
    font-weight: bold;
    color: #0078da;
}

#date {
    grid-area: date;
    display: flex;
    justify-content: flex-end;
    align-items: flex-start;
}

#humidity {
    grid-area: humidity;
    display: flex;
    justify-content: flex-start;
    align-items: flex-end;
}

#feeling {
    grid-area: feeling;
    display: flex;
    justify-content: flex-end;
    align-items: flex-end;
    white-space: nowrap;
}


@media only screen 
and (max-width: 1000px) {
    .weather-box {
        width: 400px;
        height: 250px;
    }

    i {
        font-size: 20px;
    }

    .color-size {
        font-size: 16px;
    }

    #temp {
        font-size: 45px;
    }

    #city-name {
        font-size: 22px;
    }
}

@media only screen 
and (max-width: 530px) {
    .weather-box {
        width: 300px;
        height: 175px;
    }

    i {
        font-size: 16px;
    }

    .color-size {
        font-size: 14px;
    }

    #temp {
        font-size: 35px;
    }

    #city-name {
        font-size: 16px;
    }
}

@media only screen 
and (max-width: 380px) {
    .weather-box {
        width: 240px;
    }

    i {
        font-size: 15px;
    }

    .color-size {
        font-size: 13px;
    }

    #temp {
        font-size: 28px;
    }

    #city-name {
        font-size: 14px;
    }
}
</style>