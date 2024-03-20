<script setup>
import { ref } from 'vue';
import SearchInput from './components/SearchInput.vue';
import WeatherCard from './components/WeatherCard.vue';
const places = ref([])
const addPlace=(data)=>{
  places.value.push(data)
  console.log(data)
}

const deletePlace=(name)=>{
  places.value=places.value.filter(p=>p.location.name!==name)
}

const isMobile = ref(window.innerWidth < 640);
window.addEventListener('resize', () => {
  isMobile.value = window.innerWidth < 640;
});
</script>
<template>
  <main>
    <!-- Date -->
    <div class="text-center mb-6">
      {{ new Date().toLocaleDateString('en-us', {
        weekday: 'long',
        year: 'numeric',
        month: 'long',
        day: 'numeric',
      }) }}
    </div>
<!-- Search -->
    <div>
      <SearchInput @place-data="addPlace" />

    </div>
<!-- Weather Card -->
<div :class="{ 'grid grid-cols-1 gap-4': isMobile, 'grid grid-cols-2 gap-4': !isMobile }">
    <div v-for="(place, idx) in places" :key="idx">
      <WeatherCard :place="place" @delete-place="deletePlace" />
    </div>
  </div>
  </main>

</template>