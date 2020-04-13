<template>
    <div :style="style" class="item">
    </div>
</template>

<script>
export default {
  name: 'Item',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: this.item.links[0].href,
      title: this.item.data[0].title,
    };
  },
  computed: {
    style() {
      return `backgroundImage: url("${this.photo}")
      `;
    },
  },
};
</script>

<style lang="scss" scoped>
  .item {
    width: 70vw;
    height: 250px;
    background-size: cover;
    background-position: 50%;
    background-repeat: no-repeat;
    @media(min-width: 425px) {
      width: 40vw;
    }
    @media(min-width: 768px) {
      width: 25vw;
    }
  }
</style>
