<template>
<article>
    <div class="weather-box">
        <div id="temp">temp</div>
        <div class="color-size" id="weather">weertje</div>
        <div id="city-name">New Amsterdam</div>
        <div class="color-size" id="date">date</div>
        <div class="color-size" id="humidity">humid</div>
        <div class="color-size" id="feeling">feel</div>
    </div>
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
        document.getElementById('temp').innerHTML = `${temperature}°C`;
        // TODO: ROUND DE GETAL, en daarna spatie toevoege voor celsius
        //<!-- TODO: HUMIDITY (icon tint) ICON, feel temp (icon smile)-->
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

.color-size {
    font-size: 20px;
    color: #003780;
}

#temp {
    grid-area: temp;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 65px;
    font-weight: bold;
    color: #0055c4;
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
    color: #003780;
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
}


@media only screen 
and (max-width: 1000px) {
    .weather-box {
        width: 400px;
        height: 250px;
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