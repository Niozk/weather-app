<template>
<header>
    <h1>Welcome to the weather app!</h1>
</header>
</template>

<script setup>
</script>

<style scoped>
header {
    display: flex;
    justify-content: center;
    padding-top: 100px;
}

header h1 {
    padding: 35px 50px;
    border-radius: 25px;
    font-size: 60px;
    color: white;
    background: #00ff9583;
    text-shadow: 4px 3px 0 #7A7A7A;
}

@media only screen 
and (max-width: 1000px) {
    header h1 {
        font-size: 30px;
    }
}

@media only screen 
and (max-width: 530px) {
    header h1 {
        padding: 30px 25px;
        font-size: 26px;
        text-shadow: 3px 2px 0 #7A7A7A;
    }
}

@media only screen 
and (max-width: 410px) {
    header h1 {
        padding: 25px 18px;
        font-size: 20px;
        text-shadow: 2px 2px 0 #7A7A7A;
    }
}
</style>
