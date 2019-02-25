<template>
  <div :style="style" class="item" />
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
      photo: '',
      title: this.item.data[0].title,
    };
  },
  computed: {
    style() {
      return `backgroundImage: url("${this.photo}")`;
    },
  },

  mounted() {
    this.photo = this.item.links[0].href;
  },
};
</script>

<style lang="scss" scoped>
  .item {
    min-width: 40vw;
    height: 250px;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: 50%;

    @media (min-width: 768px){
      width: 25vw;
    }
  }

</style>
