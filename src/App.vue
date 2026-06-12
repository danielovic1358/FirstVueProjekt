<script setup lang="ts">
import { onMounted, ref } from 'vue';
import axios from 'axios';

const city = ref(<string>"") 

const wjson = ref(<any>{})

const handleSubmit = async() => {
  let response = await axios.get("http://api.weatherapi.com/v1/forecast.json?key=ba1c13e7efa44e93af174636260906&q=" + city.value + "&days=7&aqi=yes&alerts=yes&lang=de")
  wjson.value = response.data
}

</script>

<template>
    <h1>Wetterapp</h1>
    <br>
    <h2>Wetterinformationen für {{ city }}:</h2>
    <input v-model="city" type="text">
    <button type="submit" v-on:click="handleSubmit">Absenden</button>
  <div v-if="wjson.forecast">
    <div v-for="value in wjson.forecast.forecastday">
      <h3>{{ value.date_epoch}}</h3>
      <p>Maximal erreichbare Temperatur: {{ value.day.maxtemp_c }}</p>
      <p>Gemeldete Wetterlage: {{ value.day.condition.text}}</p>
    </div>
  </div>
</template>

<style>
</style>
