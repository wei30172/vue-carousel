<template>
  <div class="home">
    <Carousel>
      <Slide></Slide>
    </Carousel>
  </div>
</template>

<script>
import Carousel from "../components/Carousel.vue";
import Slide from "../components/Slide.vue";

export default {
  name: "HomeView",
  components: { Carousel, Slide },
};
</script>
