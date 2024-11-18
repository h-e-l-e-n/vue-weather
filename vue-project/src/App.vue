<script setup>
import headerInfo from './components/headerInfo.vue'
import mainInfo from './components/mainInfo.vue'
import { ref, onMounted } from 'vue'
import { useWeatherStore } from './stores/currentWeather'
// import { Rain, Cloud, CloudSunny, SunLight } from '@iconoir/vue';


const weatherStore = useWeatherStore()

const getLocation = () => new Promise((resolve, reject) => {
  navigator.geolocation.getCurrentPosition((position) => {
    weatherStore.setLocation(position.coords)
    resolve(position)
  },
  (err) => {
    weatherStore.setErrorMsg = `無法取得位置：${err.message}`
    reject(err)
  }
)
})

onMounted(async() => {
  await getLocation()
  if (weatherStore.location){
    await weatherStore.fetchWeatherData()
  }
})
</script>

<template>
  <main class="bg-blue-500 flex flex-col items-center h-screen">
      <headerInfo/>
      <!-- <h1 class="text-xl text-white font-bold">{{ weatherStore.timezone }}</h1> -->
      <!-- <p class="text-sm text-gray-200">Friday, 15 November</p> -->

    <div>
      <mainInfo class="text-white"/>
      <!-- <h1 class="text-5xl font-bold text-white">目前溫度：{{ weatherStore.currentWeather.temp }}</h1> -->
      <!-- <h2 class="text-3xl font-bold text-white">體感溫度：{{ weatherStore.currentWeather.feels_like }}</h2> -->
      
    </div>
  </main>
</template>

<style scoped>

</style>
