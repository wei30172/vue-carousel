<template>
  <div class="carousel">
    <slot :currentSlide="currentSlide" />

    <!-- Navigattion -->
    <div v-if="navEnabled" class="navigate">
      <div class="carousel-arrow left">
        <ArrowLeft @click="prevSlide" />
      </div>
      <div class="carousel-arrow right">
        <ArrowRight @click="nextSlide" />
      </div>
    </div>

    <!-- Pagination -->
    <div v-if="pagintationEnabled" class="pagination">
      <span
        v-for="(slide, index) in getSlideCount"
        :key="index"
        @click="goToSlide(index)"
        class="box-shadow"
        :class="{ active: index + 1 === currentSlide }"
      />
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
  props: ["slideCount", "navigation", "pagination", "autoPlay", "duration"],

  setup(props) {
    const currentSlide = ref(1);
    const getSlideCount = toRef(props, "slideCount");

    // default setting - navigation: true, pagination: true, autoPlay: true, duration: 5000
    const navEnabled = ref(
      props.navigation === undefined ? true : props.navigation
    );
    const pagintationEnabled = ref(
      props.pagination === undefined ? true : props.pagination
    );
    const autoPlayEnabled = ref(
      props.autoPlay === undefined ? true : props.autoPlay
    );
    const duration = ref(props.duration === undefined ? 5000 : props.duration);

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

    // go to slide
    const goToSlide = (index) => {
      currentSlide.value = index + 1;
    };

    // autoplay
    const autoPlay = () => {
      setInterval(() => {
        nextSlide();
      }, duration.value);
    };

    if (autoPlayEnabled.value) {
      autoPlay();
    }

    return {
      currentSlide,
      getSlideCount,
      nextSlide,
      prevSlide,
      goToSlide,
      navEnabled,
      pagintationEnabled,
    };
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
    border-radius: 50%;
    padding: 5px;
    background-color: colors.$primary;
    color: colors.$white;
  }
}

.pagination {
  position: absolute;
  bottom: 24px;
  width: 100%;
  display: flex;
  gap: 20px;
  justify-content: center;
  align-items: center;

  span {
    cursor: pointer;
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background-color: colors.$white;

    &.active {
      background-color: colors.$primary;
    }
  }
}
</style>
