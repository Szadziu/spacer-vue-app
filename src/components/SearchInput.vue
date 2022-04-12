<template>
  <div class="searchWrapper">
    <input
      name="search"
      id="search"
      v-model="searchValue"
      @input="handleInput"
    />
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
.searchWrapper {
  display: flex;
  margin-top: 50px;
  flex-direction: column;
  width: 250px;

  input {
    height: 30px;
    border: 0;
    background: none;
    border-bottom: 1px solid white;
  }
}
</style>
