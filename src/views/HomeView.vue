<script setup>
import { ref } from "vue";
import axios from "axios";
import { useRouter } from "vue-router";
import CityList from "../components/CityList.vue";

const router = useRouter();
const mapBoxAPIKey = import.meta.env.VITE_MAPBOX_API_KEY;
const searchQuery = ref("");
const queryTimeout = ref(null);
const mapBoxSearchResults = ref(null);
const searchError = ref(null);

const getSearchResults = () => {
  clearTimeout(queryTimeout.value);
  queryTimeout.value = setTimeout(async () => {
    if (searchQuery.value !== "") {
      try {
        const result = await axios.get(
          `https://api.mapbox.com/geocoding/v5/mapbox.places/${searchQuery.value}.json?access_token=${mapBoxAPIKey}&types=place`
        );
        mapBoxSearchResults.value = result.data.features;
        //console.log(mapBoxSearchResults.value);
      } catch {
        searchError.value = true;
      }
      return;
    }
    mapBoxSearchResults.value = null;
  }, 300);
};

const previewCity = (searchResult) => {
  const [city, state] = searchResult.place_name.split(",");
  router.push({
    name: "cityView",
    params: { state: state.replaceAll(" ", ""), city: city },
    query: {
      lat: searchResult.geometry.coordinates[1],
      lng: searchResult.geometry.coordinates[0],
      preview: true,
    },
  });
};
</script>

<template>
  <main class="container text-white">
    <!--City Search bar is loaded here-->
    <div class="pt-4 mb-8 relative">
      <input
        type="text"
        v-model="searchQuery"
        @input="getSearchResults"
        name=""
        id=""
        class="py-2 px-1 w-full bg-transparent border-b focus: border-weather-hover-color focus: outline-none focus:shadow-md"
      />
      <ul
        class="absolute bg-weather-primary text-white w-full shadow-md py-2 px-1 top-[66px] z-10"
        v-if="mapBoxSearchResults"
      >
        <p class=" z-10" v-if="searchError">Sorry something went wrong</p>
        <p class=" z-10" v-if="!searchError && mapBoxSearchResults.length === 0">
          No match found...
        </p>
        <template v-else>
          <li
            v-for="searchResult in mapBoxSearchResults"
            :key="searchResult.id"
            class="py-2 cursor-pointer"
            @click="previewCity(searchResult)"
          >
            {{ searchResult.place_name }}
          </li>
        </template>
      </ul>
    </div>
    <div class="flex flex-col gap-4 bg-weather-primary p-3 rounded-md">
      <h4 class="text-xl mb-0 text-center">Saved cities</h4>
      <Suspense>
        <!--City list is loaded here-->
        <CityList />
        <template #fallback>
          <div
            class="container flex flex-col font-semibold text-white bg-weather-primary mt-5 p-5 m-auto"
          >
            <p>Loading ....</p>
          </div>
        </template>
      </Suspense>
    </div>
  </main>
</template>
