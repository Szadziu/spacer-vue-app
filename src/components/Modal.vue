<template>
  <div class="outerWrapper">
    <div class="innerWrapper">
      <div class="photo">
        <img :src="photo" alt="" />
      </div>
      <div class="description">
        <h2 class="title">{{ title }}</h2>
        <p class="description">
          {{ description }}
        </p>
      </div>
      <div class="close" @click="$emit('closeModal')" />
    </div>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Modal',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: null,
      title: null,
      description: null,
    };
  },
  mounted() {
    this.photo = this.item.links[0].href;
    this.title = this.item.data[0].title;
    this.description = this.item.data[0].description.substring(0, 200);
  },
};
</script>

<style lang="scss" scoped>
.outerWrapper {
  background: #f6f6f6;
  max-width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
}

.innerWrapper {
  display: flex;
  height: 100%;
  padding: 50px;
  justify-content: center;
  align-items: center;
  flex-direction: column;

  .photo {
    width: 100%;
    max-width: 300px;
    height: auto;
    background: black;

    img {
      width: 100%;
    }
  }

  .description {
    color: #333;

    .title {
      padding: 20px 0;
    }
  }

  .close {
    position: absolute;
    top: 20px;
    right: 20px;
    background-color: coral;
    border-radius: 50%;
    width: 30px;
    height: 30px;

    &::before {
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      position: absolute;
      border-radius: 50%;
      content: '';
      width: 20px;
      height: 20px;
      background-color: black;
    }
  }
}
</style>
