<template>
  <div class="wrapper">
    <Claim />
    <SearchInput />
  </div>
</template>

<script>
import Claim from '@/components/Claim';
import SearchInput from '@/components/SearchInput';
import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov';

export default {
  name: 'SearchView',
  components: { Claim, SearchInput },
  data() {
    return {
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleInput: debounce(function () {
      axios
        .get(`${API}/search?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>

<style lang="scss" scoped>
.wrapper {
  position: absolute;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 0;
  padding: 30px;
  width: 100%;
  background: no-repeat url('@/assets/space.jpg');
  background-size: cover;
  height: 100vh;
  background-position: 50%;
}
</style>
