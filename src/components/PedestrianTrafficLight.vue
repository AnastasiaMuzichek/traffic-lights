<script setup lang="ts">
import { shallowRef, watch } from 'vue';

const emit = defineEmits(['click']);

const props = defineProps({
    status: Boolean,
    time: {
        required: true,
        type: Number,
    },
});

const ready = shallowRef(false);
const timerId = shallowRef<number>(0);

function convert(num: number): string {
    return num.toString().padStart(2, '0');
}

function buttonClick() {
    if (!ready.value) {
        ready.value = true;

        if (!timerId.value) {
            emit('click');
        }
    }
}

watch(
    () => props.status,
    (value: boolean) => {
        if (!value && ready.value) {
            ready.value = false;
            timerId.value = setTimeout(() => {
                if (ready.value) {
                    emit('click');
                }
                timerId.value = 0;
            }, 7000);
        }
    }
);
</script>

<template>
    <div>
        <div class="base-traff">
            <div class="circle" style="position: relative">
                <div
                    class="circle-red"
                    :class="{ 'opacity-1': props.status === false }"
                >
                    <img src="../assets/images/red.png" />
                </div>
                <div class="timer" :class="{ 'opacity-1': props.status }">
                    {{ convert(props.time) }}
                </div>
            </div>
            <div class="circle">
                <div
                    class="circle-green"
                    :class="{ 'opacity-1': props.status }"
                >
                    <img src="../assets/images/green.png" />
                </div>
            </div>
        </div>
        <div class="block-button">
            <button
                class="button"
                @click="buttonClick"
                :class="{ 'button-after': ready }"
            >
                ЖДИТЕ
            </button>
        </div>
    </div>
</template>

<style>
.button {
    width: 90px;
    height: 90px;
    border-radius: 50%;
    background-color: rgb(121, 146, 146);
    border: none;
    color: rgb(235, 231, 43);
    padding: 15px 32px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    font-size: 16px;
    margin-top: 50px;
}
button:focus,
button:focus-visible {
    outline: 4px auto -webkit-focus-ring-color;
}

/* стили для кнопки после нажатия ->   тени внутри после нажатия*/
.button-after {
    font-weight: 800;
    box-shadow: inset 0px 10px 20px 2px rgba(0, 0, 0, 0.25);
}

.block-button {
    display: flex;
    justify-content: center;
}

.base-traff {
    width: 250px;
    height: 380px;
    background: rgb(1, 1, 5);
    background: linear-gradient(
        125deg,
        rgba(1, 1, 5, 1) 0%,
        rgba(72, 61, 77, 1) 57%,
        rgba(130, 101, 116, 1) 100%
    );
    border-radius: 50px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 30px 75px;
    flex-direction: column;
}

.timer {
    position: absolute;
    inset: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 80px;
    color: rgb(142, 230, 11);
}

img {
    width: 60%;
    height: 100%;
}
</style>
