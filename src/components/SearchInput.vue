<template>
  <div class="searchWrapper">
    <input
      name="search"
      id="search"
      :value="value"
      @input="handleChange"
      :class="{ dark }"
    />
  </div>
</template>

<script>
export default {
  name: 'SearchInput',
  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
.searchWrapper {
  display: flex;
  margin-top: 50px;
  flex-direction: column;
  width: 250px;

  input {
    color: white;
    text-align: center;
    font-size: 18px;
    font-weight: 300;
    height: 30px;
    border: 0;
    background: none;
    border-bottom: 1px solid white;
    transition: box-shadow 0.5s;
  }

  input:focus {
    outline: none;
    box-shadow: 0 10px 20px -8px rgba(255, 255, 255, 0.3);
  }

  .dark {
    color: black;
  }
}
</style>
