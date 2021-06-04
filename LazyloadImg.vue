<template>
  <div
    ref="outBox"
    class="outer-box"
    @scroll="scrollListener"
  >
    <!-- key用index是不对的，但是先将就 -->
    <img
      v-for="(item,index) in imgsSrc"
      :src="defaultImg"
      :key="index"
    >
  </div>
</template>

<script>
export default {
  name: 'LazyloadImg',
  props: {
    imgsSrc: {
      type: Array
    },
    defaultImg: ''
  },
  methods: {
    scrollListener() {
      let arrImgs = this.$refs.outBox.children;
      for (let i = 0; i < arrImgs.length; i++) {
        if (arrImgs[i].offsetTop< (this.$refs.outBox.scrollTop + this.$refs.outBox.clientHeight)&&arrImgs[i].src==this.defaultImg) {
          console.log(i);
          arrImgs[i].src = this.imgsSrc[i];
        }
      }
    }
  }
};
</script>

<style scoped>
.outer-box {
  width: 200px;
  height: 150px;
  overflow: scroll;
}
</style>