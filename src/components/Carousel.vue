<template>
  <div class="carousel">
    <slot :currentSlide="currentSlide" />

    <!-- Navigattion -->
    <div class="navigate">
      <div class="carousel-arrow left">
        <ArrowLeft />
      </div>
      <div class="carousel-arrow right">
        <ArrowRight />
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import ArrowLeft from "@/features/Carousel/ArrowLeft.vue";
import ArrowRight from "@/features/Carousel/ArrowRight.vue";

export default {
  name: "CarouselComponent",
  components: { ArrowLeft, ArrowRight },
  setup() {
    const currentSlide = ref(0);

    return { currentSlide };
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
    color: #fff;
  }
}
</style>
