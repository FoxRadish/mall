<template>
  <swiper class="detail-swiper">
      <swiper-item v-for="item in topImages" :key="item">
          <img :src="item" alt="">
      </swiper-item>
  </swiper>
</template>

<script>
import Swiper from '../../../components/common/Swiper/Swiper.vue'
import SwiperItem from '../../../components/common/Swiper/Swiper_item.vue'
  

  export default {
    name: "DetailSwiper",
    components:{
      Swiper,
      SwiperItem,
    },
    props: {
      topImages: {
        type: Array,
        default() {
          return []
        }
      }
    }
  }
</script>

<style scoped>
  .detail-swiper {
    height: 250px;
    overflow: hidden;
  }
</style>
