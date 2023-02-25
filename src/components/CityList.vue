<template>
  <div v-for="city in savedCities" :key="city.id" class="glass-shade p-5 z-0">
    <CityCard :city="city" @click="goToCity(city)" />
  </div>

  <p v-if="savedCities.length === 0" class="text-center">
    No locations added. To start tracking a location, search in the field above.
  </p>
</template>

<script setup>
import axios from "axios";
import { ref } from "vue";
import { useRouter } from "vue-router";
import CityCard from "../components/CityCard.vue";

const openWeatherAPIKey = import.meta.env.VITE_OPEN_WEATHER_API_KEY;

const savedCities = ref([]);
const getCities = async () => {
  if (localStorage.getItem("savedCities")) {
    //get the cities from the local storage
    savedCities.value = JSON.parse(localStorage.getItem("savedCities"));
    //get the request url for each city
    const requests = [];
    savedCities.value.forEach((city) => {
      requests.push(
        axios.get(
          `https://api.openweathermap.org/data/3.0/onecall?lat=${city.coords.lat}&lon=${city.coords.lng}&exclude={part}&appid=${openWeatherAPIKey}&units=metric`
        )
      );
    });
    //wait for all the promises to be fullfilled
    const weatherData = await Promise.all(requests);
    weatherData.forEach((value, index) => {
      savedCities.value[index].weather = value.data;
    });
  }
};
await getCities();
const router = useRouter();
const goToCity = (city) => {
  router.push({
    name: "cityView",
    params: {
      state: city.state,
      city: city.city,
    },
    query: {
      id: city.id,
      lat: city.coords.lat,
      lng: city.coords.lng,
    },
  });
};
</script>
