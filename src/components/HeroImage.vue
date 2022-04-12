<template>
  <div class="heroImage"></div>
</template>

<script>
export default {
  name: 'HeroImage',
};
</script>

<style lang="scss" scoped>
.heroImage {
  width: 100%;
  height: 100vh;
  position: fixed;
  top: 0;
  z-index: -1;
  background: no-repeat url('@/assets/space.jpg');
  background-size: cover;
  height: 100vh;
  background-position: 50%;
}
</style>
