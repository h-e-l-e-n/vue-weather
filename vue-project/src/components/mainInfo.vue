<script setup>
import { Rain, Cloud, CloudSunny, SunLight } from '@iconoir/vue'
import { useWeatherStore } from '../stores/currentWeather'
import { storeToRefs } from 'pinia'

const weatherStore = useWeatherStore()
const { currentWeather } = storeToRefs(weatherStore)
</script>
<template>
    <div class="flex flex-col gap-y-2 items-center">
        <div v-if="currentWeather">        
            <h1 class="text-2xl font-bold text-white">目前溫度：{{ currentWeather.temp }}</h1>
            <img :src="`https://openweathermap.org/img/wn/${currentWeather.weather[1].icon}.png`" class="w-20 h-20">
            <p class="text-sm text-gray-200">{{ currentWeather.weather[1].description }}</p>
        </div>
        <div v-else>
            <p class="text-2xl font-bold text-white">29.99</p>
            <p class="text-sm text-gray-200">cloud</p>
        </div>

    </div>

</template>