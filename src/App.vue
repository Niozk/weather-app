<template>
    <Header class="intro"/>
    <Nav class="intro"/>
    <WeatherBox />
    <ErrorPopup />
</template>

<script setup>
import Header from './components/Header.vue'
import Nav from './components/Nav.vue'
import WeatherBox from './components/WeatherBox.vue'
import ErrorPopup from './components/ErrorPopup.vue'
import { onMounted } from 'vue';
import { animate, stagger, spring } from "motion"

let viewportWidth = window.innerWidth || document.documentElement.clientWidth;
let initialScale = (viewportWidth <= 600) ? 1 : 2;

onMounted(() => {
    animate(
        ".intro",
        { scale: [initialScale, 1] },
        { 
            easing: spring(),
            delay: stagger(0.1)
        }
    )
});
</script>

<style scoped>
</style>
