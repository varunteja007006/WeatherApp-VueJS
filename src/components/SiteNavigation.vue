<template>
  <header class="sticky top-0 bg-weather-primary shadow-lg">
    <nav
      class="container flex flex-col sm:flex-row items-center gap-4 text-white py-2"
    >
      <RouterLink :to="{ name: 'home' }">
        <div class="flex items-center gap-4">
          <i class="fa-regular fa-sun text-2xl"></i>
          <p>Weather App</p>
        </div>
      </RouterLink>
      <div class="flex items-center gap-3 flex-1 justify-end">
        <i
          class="fa-solid fa-circle-info text-xl hover:text-weather-hover-color duration-150 cursor-pointer"
          @click="toggleModal"
        ></i>
        <i
          class="fa-solid fa-plus text-xl hover:text-weather-hover-color duration-150 cursor-pointer"
        ></i>
      </div>

      <BaseModal :modalActive="modalActive" @close-modal="toggleModal">
        <h1 class="text-black text-center">Hello Frends</h1>
        <p class="p-4 text-justify">
          Aute ullamco do in anim ut sint fugiat ea non. Nisi veniam pariatur
          reprehenderit qui proident cupidatat consectetur nulla proident
          occaecat sit sit labore. Id incididunt pariatur tempor nostrud enim
          aliquip laborum magna nisi in exercitation reprehenderit. Qui occaecat
          aliqua et commodo sit dolor minim anim dolore exercitation ex amet
          non.
        </p>
        <p class="p-4 text-justify">
          Lorem, ipsum dolor sit amet consectetur adipisicing elit.
          Reprehenderit quisquam quos temporibus libero sint maxime, ipsum culpa
          soluta non, magni dolore cupiditate quasi eaque dolorem illo, quae
          ipsam repudiandae magnam.
        </p>
        <p class="p-4 text-justify">
          Duis dolore magna esse labore sint in nostrud proident qui deserunt
          voluptate ipsum.
        </p></BaseModal
      >
    </nav>
  </header>
</template>

<script setup>
import { ref } from "vue";
import { RouterLink } from "vue-router";
import BaseModal from "./BaseModal.vue";

const modalActive = ref(null);
const toggleModal = () => {
  modalActive.value = !modalActive.value;
};
</script>
