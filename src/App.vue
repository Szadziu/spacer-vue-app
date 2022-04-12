<template>
  <div :class="[{ flexStart: step === 1 }, 'wrapper']">
    <transition name="slide">
      <img
        src="@/assets/galaxy.png"
        alt="logo"
        class="logo"
        v-if="step === 1"
      />
    </transition>
    <transition name="fade">
      <HeroImage v-if="step === 0" />
    </transition>
    <Claim v-if="step === 0" />
    <SearchInput
      v-model="searchValue"
      @input="handleInput"
      :dark="step === 1"
    />
    <div class="results" v-if="results && !loading && step === 1">
      <Item
        v-for="item in results"
        :item="item"
        :key="item.data[0].nasa_id"
        @click.native="handleModalOpen(item)"
      />
    </div>
    <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false" />
  </div>
</template>

<script>
import Claim from '@/components/Claim';
import SearchInput from '@/components/SearchInput';
import HeroImage from '@/components/HeroImage';
import Item from '@/components/Item';
import Modal from '@/components/Modal';
import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov';

export default {
  name: 'App',
  components: { Claim, SearchInput, HeroImage, Item, Modal },
  data() {
    return {
      modalOpen: false,
      modalItem: null,
      loading: false,
      step: 0,
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleInput: debounce(function () {
      this.loading = true;
      axios
        .get(`${API}/search?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          this.loading = false;
          this.step = 1;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),

    // eslint-disable-next-line no-unused-vars
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },
  },
};
</script>

<style lang="scss">
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Monteserrat', sans-serif;
}

.fade-enter,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.slide-enter,
.slide-leave-active {
  transition: margin-top 0.3s ease;
}

.slide-enter,
.slide-leave-to {
  margin-top: -50px;
}

.wrapper {
  position: relative;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 0;
  padding: 30px;
  width: 100%;

  &.flexStart {
    justify-content: flex-start;
  }
}

.results {
  width: 100%;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-gap: 20px;
  margin-top: 50px;
}

.logo {
  position: absolute;
  top: -75px;
}
</style>
