<template>
  <div class="home">
    <Carousel
      class="carousel"
      v-slot="{ currentSlide }"
      :slideCount="slideCount"
    >
      <Slide v-for="(slide, index) in carouselSlides" :key="index">
        <div v-show="currentSlide === index + 1" class="slide-info">
          <img :src="require(`../assets/slide-bg/${slide}.jpg`)" />
        </div>
      </Slide>
    </Carousel>
  </div>
</template>

<script>
import { ref } from "vue";
import Carousel from "@/components/Carousel.vue";
import Slide from "@/components/Slide.vue";

export default {
  name: "HomeView",
  components: { Carousel, Slide },
  setup() {
    const carouselSlides = ref(["slide-bg1", "slide-bg2", "slide-bg3"]);
    const slideCount = carouselSlides.value.length;

    return { carouselSlides, slideCount };
  },
};
</script>

<style lang="scss" scoped>
.carousel {
  position: relative;
  width: 100%;
  height: 100vh;

  .slide-info {
    position: absolute;
    width: 100%;
    height: 100%;

    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
  }
}
</style>
