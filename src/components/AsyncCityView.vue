<template>
  <div class="container mb-2">
    <div
      v-if="route.query.preview"
      class="text-white mt-1 p-5 text-center bg-weather-primary flex flex-col rounded-lg"
    >
      <!--Banner-->
      <div
        class="text-white mt-1 mb-1 p-5 text-center bg-weather-primary flex flex-col rounded-lg"
      >
        <p>
          You are currently previewing this city, click the "+" start tracking
          this city.
        </p>
      </div>
    </div>
    <!--Weather Overview-->
    <div
      class="text-white mt-1 p-5 text-center bg-weather-primary flex flex-col rounded-lg"
    >
      <h1 class="mb-3">{{ route.params.city }}</h1>
      <h1 class="text-6xl font-semibold mb-3">
        {{ Math.round(weatherData.current.temp) }}&deg;c
      </h1>
      <p class="mb-3">
        Feels like {{ Math.round(weatherData.current.feels_like) }}&deg;
      </p>
      <p class="mb-1">
        {{
          timedate[0] +
          ", " +
          timedate[1] +
          " " +
          timedate[2] +
          " " +
          timedate[3]
        }}
      </p>
      <p class="mb-1">
        {{ timedate[4].split(":")[0] }}:
        {{ timedate[4].split(":")[1] }}
      </p>
      <p class="mt-2">
        {{ weatherData.timezone }}
      </p>
      <p class="capitalize mt-3">
        {{ weatherData.current.weather[0].description }}
      </p>
      <img
        class="w-1/4 h-auto m-auto text-white"
        :src="`http://openweathermap.org/img/wn/${weatherData.current.weather[0].icon}@2x.png`"
        alt=""
      />
      <hr class="border-white border-opacity-10 border w-full" />
      <!-- Hourly Weather -->
      <div class="max-w-screen-md w-full py-12">
        <div class="mx-8 text-white">
          <h2 class="mb-4">Hourly Weather</h2>
          <div class="flex gap-10 overflow-x-scroll">
            <div
              v-for="hourData in weatherData.hourly"
              :key="hourData.dt"
              class="flex flex-col gap-4 items-center"
            >
              <p class="whitespace-nowrap text-md">
                {{
                  new Date(hourData.dt * 1000)
                    .toString()
                    .split(" ")[4]
                    .split(":")[0]
                }}
                :
                {{
                  new Date(hourData.dt * 1000)
                    .toString()
                    .split(" ")[4]
                    .split(":")[1]
                }}
              </p>
              <img
                class="w-auto h-[50px] object-cover"
                :src="`http://openweathermap.org/img/wn/${hourData.weather[0].icon}@2x.png`"
                alt=""
              />
              <p class="text-xl">{{ Math.round(hourData.temp) }}&deg;</p>
            </div>
          </div>
        </div>
      </div>
      <hr class="border-white border-opacity-10 border w-full" />
      <!-- Weekly Weather -->
      <div class="max-w-screen-md w-full py-12">
        <div class="mx-8 text-white">
          <h2 class="mb-4">7 Day Forecast</h2>
          <div
            v-for="day in weatherData.daily"
            :key="day.dt"
            class="flex items-center"
          >
            <p class="flex-1">
              {{
                new Date(day.dt * 1000).toLocaleDateString("en-us", {
                  weekday: "long",
                })
              }}
            </p>
            <img
              class="w-[50px] h-[50px] object-cover"
              :src="`http://openweathermap.org/img/wn/${day.weather[0].icon}@2x.png`"
              alt=""
            />
            <div class="flex gap-2 flex-1 justify-end">
              <p>H: {{ Math.round(day.temp.max) }}</p>
              <p>L: {{ Math.round(day.temp.min) }}</p>
            </div>
          </div>
        </div>
      </div>
      <hr class="border-white border-opacity-10 border w-full" />
      <div
        class="flex gap-2 p-5 text-white cursor-pointer duration-150 text-center self-center align-middle hover:bg-orange-500 hover:text-black hover:font-semibold rounded-full mt-5 " @click="removeCity"
      >
        <i class="fa-sharp fa-solid fa-trash" ></i> Remove
        city
      </div>
    </div>
  </div>
</template>

<script setup>
import axios from "axios";
import { useRoute, useRouter } from "vue-router";

const route = useRoute();
const openWeatherAPIKey = import.meta.env.VITE_OPEN_WEATHER_API_KEY;
const getWeatherData = async () => {
  try {
    const weatherData = await axios.get(
      `https://api.openweathermap.org/data/3.0/onecall?lat=${route.query.lat}&lon=${route.query.lng}&appid=${openWeatherAPIKey}&units=metric`
    );
    return weatherData.data;
  } catch (error) {
    console.log(error);
  }
};

const weatherData = await getWeatherData();
const timedate = new Date(weatherData.current.dt * 1000).toString().split(" ");

const router = useRouter();
const removeCity = () => {
  const cities = JSON.parse(localStorage.getItem("savedCities"));
  const updatedCities = cities.filter((city) => {
    city.id !== route.query.id;
  });
  localStorage.setItem("savedCities", JSON.stringify(updatedCities));
  router.push({
    name: "home",
  });
};
</script>
