<script setup lang="ts">
import type { PropType } from 'vue';
import { EnumTrafficColor } from '../constants';

const props = defineProps({
    color: {
        required: true,
        type: Object as PropType<EnumTrafficColor>,
    },
});
</script>

<template>
    <div class="base">
        <div class="circle">
            <div
                class="circle-red"
                :class="{ 'opacity-1': props.color === EnumTrafficColor.red }"
            ></div>
        </div>
        <div class="circle">
            <div
                class="circle-yellow"
                :class="{
                    'opacity-1': props.color === EnumTrafficColor.yellow,
                }"
            ></div>
        </div>
        <div class="circle">
            <div
                class="circle-green"
                :class="{ 'opacity-1': props.color === EnumTrafficColor.green }"
            ></div>
        </div>
    </div>
</template>

<style>
* {
    box-sizing: border-box;
}

.base {
    width: 350px;
    height: 700px;
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

h1 {
    font-family: cursive;
}

.circle {
    width: 200px;
    height: 200px;
    border-radius: 50%;
    background: slategrey;

    div {
        opacity: 0;
    }

    div.opacity-1 {
        opacity: 1;
    }
}

.circle-red {
    background: rgb(156, 8, 15);
    background: linear-gradient(
        125deg,
        rgba(156, 8, 15, 1) 0%,
        rgba(223, 34, 21, 1) 56%,
        rgba(201, 112, 23, 1) 100%
    );
    width: 200px;
    height: 200px;
    border-radius: 50%;
    border-style: dotted;
    box-shadow: 0 0 25px brown;
    /* эффект свечения вокрук блока!*/
}

.circle-yellow {
    background: rgb(238, 152, 11);
    background: linear-gradient(
        125deg,
        rgba(238, 152, 11, 1) 0%,
        rgba(232, 173, 32, 1) 56%,
        rgba(221, 222, 7, 1) 100%
    );
    width: 200px;
    height: 200px;
    border-radius: 50%;
    border-style: dotted;
    box-shadow: 0 0 25px rgb(231, 217, 12);
}

.circle-green {
    background: rgb(32, 88, 5);
    background: linear-gradient(
        125deg,
        rgba(32, 88, 5, 1) 0%,
        rgba(49, 153, 7, 1) 56%,
        rgba(132, 233, 12, 1) 100%
    );
    width: 200px;
    height: 200px;
    border-radius: 50%;
    border-style: dotted;
    box-shadow: 0 0 25px rgb(40, 182, 47);
}
</style>
