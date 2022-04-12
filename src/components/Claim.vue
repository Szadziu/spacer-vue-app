<template>
  <div class="claimWrapper">
    <h1 class="claim">spacer</h1>
    <p class="subclaim">
      Begin your journey through our amazing galaxy, and discover places you
      never even heard of.
    </p>
    <p class="subclaim">Type anything space-related to start.</p>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Claim',
};
</script>

<style lang="scss" scoped>
.claimWrapper {
  display: flex;
  text-align: center;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  color: crimson;
}

.claim {
  text-transform: uppercase;
  font-size: 50px;
  margin: 0;
}

.subclaim {
  margin: 25px 0 0;
  font-size: 16px;
}
</style>
