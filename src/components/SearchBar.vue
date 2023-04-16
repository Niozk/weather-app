<template>
<form class="search-bar" @submit.prevent="TESTESTEST">
    <input type="text" class="search-text" name="search-text" placeholder="Enter the location">
    <button type="submit" class="search-button">
        <i class="icon-search"></i>
    </button>
</form>
</template>

<script setup>

</script>

<style scoped>
form {
    display: flex;
    padding-top: 45px;
    width: 35%;
}

.search-text {
    padding: 5px;
    width: 100%;
    height: 26px;
    border: 3px solid #63d2e0;
    border-radius: 5px 0 0 5px;
    outline: none;
    transition: border-color 0.3s ease-in-out;
}

.search-text:focus{
    border: 3px solid #09acc2;
}

.search-button {
    width: 40px;
    height: 42px;
    background: #63d2e0;
    color: white;
    font-size: 20px;
    text-align: center;
    cursor: pointer;
    border: 1px solid #63d2e0;
    border-radius: 0 5px 5px 0;
}

@media only screen 
and (max-width: 1000px) {
    form {
        width: 45%;
    }
}

@media only screen 
and (max-width: 530px) {
    form {
        width: 65%;
    }

    .search-text {
        height: 18px;
    }

    .search-button {
        height: 34px;
    }
}
</style>