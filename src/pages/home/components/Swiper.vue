<template>
  <div class="wrapper">
    <swiper :options="swiperOption">
      <swiper-slide v-for="item of swiperList" :key="item.id"><img class="swiper-image"
                                                                   :src="item.imgUrl"
                                                                   alt=""></swiper-slide>
      <div class="swiper-pagination" slot="pagination"></div>
    </swiper>
  </div>
</template>

<script>
export default {
  name: 'HomeSwiper',
  data () {
    return {
      swiperOption: {
        // some swiper options/callbacks
        // 所有的参数同 swiper 官方 api 参数
        // ...
        pagination: '.swiper-pagination',
        loop: true
      },
      swiperList: [{
        id: '0001',
        imgUrl: 'https://imgs.qunarzz.com/p/tts6/1703/a1/bf7e61143113d02.jpg_r_390x260x90_3f15ccec.jpg'
      }, {
        id: '0002',
        imgUrl: 'https://img1.qunarzz.com/p/tts0/1703/75/6d627693f77b1b02.jpg_r_640x420x90_fbad911b.jpg'
      }]
    }
  }
}
</script>

<style lang="stylus" scoped>
  .wrapper >>> .swiper-pagination-bullet-active
    background: #fff

  .wrapper
    width: 100%;
    height: 31.25vw
    background-color: #eee

    .swiper-image
      width: 100%;
      height: 31.25vw
</style>
