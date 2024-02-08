<template>
  <div class="request-container">
    <h2>Random Cute Cat Images</h2>
    <swiper :navigation="true" :modules="modules" class="mySwiper">
      <swiper-slide v-for="(image, index) in images" :key="index">
        <div class="card">
          <img :src="image.url" :alt="`Image ${index + 1}`" class="img">
        </div>
      </swiper-slide>
    </swiper>
  </div>
</template>

<script setup>
import {ref, onMounted} from 'vue';
import {Swiper, SwiperSlide} from 'swiper/vue';
import 'swiper/css';
import 'swiper/css/navigation';
import {Navigation} from 'swiper/modules';
import 'swiper/swiper-bundle.css';

const modules = [Navigation];
const URL = 'https://api.thecatapi.com/v1/images/search?limit=10';
const images = ref([]);

async function fetchImages() {
  try {
    const response = await fetch(URL);
    images.value = await response.json();
  } catch (error) {
    alert('сервер не найден 404');
  }
}

onMounted(() => {
  fetchImages();
});
</script>

<style scoped lang="stylus">
@import '../src/styles/requests.styl'
</style>
