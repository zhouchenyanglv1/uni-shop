<template>
  <view>
    <swiper :indicator-dots="true" :autoplay="true" :circular="true" :duration="1000" :interval="2000">
      <navigator class="swiper-item"  v-for="item in swiperList" key="item.goods_id">
        <swiper-item>
          <image :src="item.image_src"></image>
        </swiper-item>
      </navigator>
    </swiper>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        swiperList: []
      };
    },
    methods: {
      async getSwiperList() {
        const {
          data
        } = await uni.$http.get('/api/public/v1/home/swiperdata')
        if (data.meta.status !== 200) {
          return uni.$showMsg
        }
        this.swiperList = data.message
      }
    },
    onLoad() {
      this.getSwiperList()
    }
  }
</script>

<style lang="scss">
  swiper {
    height: 330rpx;
  
  .swiper-item {
      image {
        width: 100%;
        height: 100%;
      }
    }
  }
</style>
