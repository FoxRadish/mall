<template>
  <div>
    <deatail-navbar/>
    <detail-swiper :topImages="topImages"/>
    <detail-base-info :goods="goods"/>
  </div>
</template>

<script>
import DeatailNavbar from './ChildComs/DeatailNavbar.vue';
import DetailSwiper from './ChildComs/DetailSwiper.vue';
import {getDetail,Goods} from '../../network/detail';
import DetailBaseInfo from './ChildComs/DetailBaseInfo.vue';
export default {
  name:'Detail',
  data () {
    return {
      topImages:[],
      goods:{},
    }
  },
  components: { DeatailNavbar, DetailSwiper, DetailBaseInfo },
    created(){
      this.iid = this.$route.query.iid
      // 2.根据iid请求详细数据
      getDetail(this.iid).then(res => {
        // console.log(res);
        // 1.获取数据
        const data = res.result;
        // 2.取出顶部轮播图的数据
        this.topImages = data.itemInfo.topImages;
        this.goods = new Goods(data.itemInfo,data.columns,data.shopInfo.services);
      });
    }
}
</script>

<style>

</style>