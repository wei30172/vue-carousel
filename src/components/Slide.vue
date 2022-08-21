<template>
  <div class="slide">
    <transition name="slide-animation">
      <slot />
    </transition>
  </div>
</template>

<script>
export default {
  name: "SlideComponent",
};
</script>

<style lang="scss" scoped>
.slide-animation-enter-from,
.slide-animation-leave-to {
  opacity: 0;
}
.slide-animation-enter-to,
.slide-animation-leave-from {
  opacity: 1;
}
.slide-animation-enter-active,
.slide-animation-leave-active {
  transition: opacity 0.6s ease-in-out;
}
</style>
