<script setup>
import { storeToRefs } from 'pinia';
import { useWeatherStore } from '../stores/currentWeather'
import dayjs from 'dayjs'
import { ref } from 'vue'

const weatherStore = useWeatherStore()
const { city } = storeToRefs(weatherStore)
console.log(city);

const now = dayjs()
const currentDate = ref(now.format('dddd, D MMMM'))


</script>
<template>
    <div class="flex flex-col gap-y-2 items-center">
        <h1 class="text-xl text-white font-bold">{{ city }}</h1>
        <p class="text-sm text-gray-200">{{ currentDate }}</p>
    </div>

</template>
