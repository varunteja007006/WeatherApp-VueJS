<template>
  <div>
    <Suspense>
      <AsyncCityView></AsyncCityView>
      <template #fallback>
        <div class=" container flex flex-col font-semibold text-white bg-weather-primary mt-5 p-5 m-auto">
          <p>Loading .... </p>
        </div>
      </template>
    </Suspense>
  </div>
</template>

<script setup>
import AsyncCityView from "../components/AsyncCityView.vue";
</script>
