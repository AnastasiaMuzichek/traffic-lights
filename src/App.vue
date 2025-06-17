<script setup lang="ts">
import TrafficLights from './components/TrafficLights.vue';
import PedestrianTrafficLight from './components/PedestrianTrafficLight.vue';
import { shallowRef, onMounted } from 'vue';
import { EnumTrafficColor } from './constants';

const enum EnumTrafficInterval {
    empty = 0,
    red = 5,
    yellow = 1,
    green = 3,
}

const flag = shallowRef(false);
const timeId = shallowRef();
const timer = shallowRef(EnumTrafficInterval.green);
const timerPedestrian = shallowRef(0);
const color = shallowRef(EnumTrafficColor.green);
const showed = shallowRef(false);

function process() {
    timer.value--;
    timerPedestrian.value--;
    if (timer.value !== EnumTrafficInterval.empty) {
        return;
    }
    if (color.value === EnumTrafficColor.red) {
        color.value = EnumTrafficColor.yellow;
        timer.value = EnumTrafficInterval.yellow;
    } else if (color.value === EnumTrafficColor.yellow) {
        color.value = EnumTrafficColor.green;
        timer.value = EnumTrafficInterval.green;
        clearInterval(timeId.value);
    } else {
        color.value = EnumTrafficColor.red;
        timer.value = EnumTrafficInterval.red;
        timerPedestrian.value =
            EnumTrafficInterval.yellow + EnumTrafficInterval.red;
    }
}

function handleClick() {
    if (flag.value === false) {
        flag.value = true;
    }
    timeId.value = setInterval(process, 1000);
}

onMounted(() => {
    setTimeout(() => {
        showed.value = true;
    }, 1500);
});
</script>

<template>
    <div>
        <h1>СВЕТОФОР</h1>
        <Transition>
            <div style="display: flex; gap: 32px" v-show="showed">
                <TrafficLights :color="color" v-model="flag"></TrafficLights>
                <PedestrianTrafficLight
                    :status="color !== EnumTrafficColor.green"
                    :time="timerPedestrian"
                    @click="handleClick"
                ></PedestrianTrafficLight>
            </div>
        </Transition>
    </div>
</template>

<style scoped>
.v-enter-active,
.v-leave-active {
    transition: opacity 1.5s ease;
}

.v-enter-from,
.v-leave-to {
    opacity: 0;
}
</style>
