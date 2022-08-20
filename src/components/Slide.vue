<template>
  <div class="slide">
    <transition name="slide">
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
.slide-enter-from,
.slide-leave-to {
  opacity: 0;
}
.slide-enter-to,
.slide-leave-from {
  opacity: 1;
}
.slide-enter-active,
.slide-leave-active {
  transition: opacity 0.6s ease-in-out;
}
</style>
