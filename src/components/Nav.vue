<template>
<nav>
    <h2>Know the weather anywhere, at anytime</h2>
    <SearchBar />
</nav>
</template>

<script setup>
import SearchBar from './SearchBar.vue'
</script>

<style scoped>
nav {
    display: flex;
    align-items: center;
    flex-direction: column;
}

nav h2 {
    padding: 15px 25px;
    border-radius: 25px;
    font-size: 26px;
    color: #ffffff;
    background: #008cff;
}

@media only screen 
and (max-width: 1000px) {
    nav h2 {
        font-size: 18px;
    }
}

@media only screen 
and (max-width: 530px) {
    nav h2 {
        padding: 10px 20px;
        font-size: 14px;
    }
}

@media only screen 
and (max-width: 410px) {
    nav h2 {
        font-size: 12px;
    }
}
</style>
