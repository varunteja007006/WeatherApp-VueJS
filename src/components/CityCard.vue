<template>
  <div class="flex flex-row z-0">
    <div class="flex flex-col flex-1">
      <h5 class="text-xl">{{ city.city }}</h5>
      <h6 class="text-sm">{{ city.state }}</h6>
    </div>
    <div class="flex flex-col">
      <p class="text-3xl self-end">
        {{ Math.round(city.weather.current.temp) }}&deg;c
      </p>
      <p class="text-xs">{{ city.weather.current.weather[0].description }}</p>
    </div>
    <div class="flex flex-col items-center">
      <img
        class="w-auto h-[50px] object-cover self-center"
        :src="`http://openweathermap.org/img/wn/${city.weather.current.weather[0].icon}@2x.png`"
        alt=""
      />
    </div>
  </div>
</template>

<script setup>
defineProps({
  city: {
    type: Object,
    default: () => {},
  },
});
</script>
