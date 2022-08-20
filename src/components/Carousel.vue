<template>
  <div class="carousel">
    <slot :currentSlide="currentSlide" />

    <!-- Navigattion -->
    <div class="navigate">
      <div class="carousel-arrow left">
        <ArrowLeft @click="prevSlide" />
      </div>
      <div class="carousel-arrow right">
        <ArrowRight @click="nextSlide" />
      </div>
    </div>
  </div>
</template>

<script>
import { ref, toRef } from "vue";
import ArrowLeft from "@/features/Carousel/ArrowLeft.vue";
import ArrowRight from "@/features/Carousel/ArrowRight.vue";

export default {
  name: "CarouselComponent",
  components: { ArrowLeft, ArrowRight },
  props: ["slideCount"],

  setup(props) {
    const currentSlide = ref(1);
    const getSlideCount = toRef(props, "slideCount");

    // next slide
    const nextSlide = () => {
      if (currentSlide.value === getSlideCount.value) {
        currentSlide.value = 1;
        return;
      }
      currentSlide.value += 1;
    };

    // prev slide
    const prevSlide = () => {
      if (currentSlide.value === 1) {
        currentSlide.value = 1;
        return;
      }
      currentSlide.value -= 1;
    };

    return { currentSlide, getSlideCount, nextSlide, prevSlide };
  },
};
</script>

<style lang="scss" scoped>
@use "../styles/mixin/colors" as colors;

.navigate {
  height: 100%;
  width: 100%;
  padding: 0 20px;
  position: absolute;
  display: flex;
  justify-content: space-between;
  align-items: center;
  .carousel-arrow {
    width: 40px;
    height: 40px;
    border-radius: 100%;
    padding: 5px;
    background-color: colors.$primary;
    color: colors.$white;
  }
}
</style>
