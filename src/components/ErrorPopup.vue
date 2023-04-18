<template>
<Teleport to="body">
    <Transition name="fade" mode="out-in" appear>
        <div v-if="store.popup" class="popup">
            <p>Please enter a valid location</p>
            <button @click="closePopup"><i class="icon-remove"></i></button>
        </div>
    </Transition>
</Teleport>
</template>

<script setup>
import { store } from '../store.js'

function closePopup() {
    store.popup = false;
}
</script>

<style scoped>
.popup {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 15px;
    position: fixed;
    z-index: 999;
    left: 50%;
    top: 45%;
    transform: translate(-50%, -50%);
    width: 300px;
    height: 75px;
    background-color: white;
    border-radius: 15px;
    box-shadow: 0 3px 10px #00000033;
}

button {
    height: 35px;
    border: 0;
    cursor: pointer;
    background-color: transparent;
}

p {
    color: #0062b3;
}

i {
    font-size: 20px;
    color: #004074;
}

.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}

@media only screen 
and (max-width: 380px) {
    .popup {
        width: 260px;
        gap: 4px;
    }
}
</style>