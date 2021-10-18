<template>
  <div class="detail">
    <deatail-navbar class="detail-nav-bar" @titleClick="titleClick" ref="detailnavbar"/>
    <div class="detail-container" @scroll="scrollto" ref="detail-container">
      <detail-swiper :topImages="topImages" class="detail-swiper" />
      <detail-base-info :goods="goods" class="detail-base" />
      <detail-shop-info :shop="shop" class="detail-shop" />
      <detail-goods-info :detail-info="detailInfo" class="detail-goods" />
      <detail-param-info :param-info="paramInfo" class="param-info" />
      <detail-comment-info :comment-info="commentInfo" class="comment-info" />
      <shop-list :shop="recommends" class="shop-list" />
    </div>
    <detail-bottom-bar class="bottom-bar" />
    <backtop class="backtop" @click.native="BackTop" v-show="display"/>
  </div>
</template>

<script>
import DeatailNavbar from "./ChildComs/DeatailNavbar.vue";
import DetailSwiper from "./ChildComs/DetailSwiper.vue";
import DetailBaseInfo from "./ChildComs/DetailBaseInfo.vue";
import DetailShopInfo from "./ChildComs/DetailShopInfo.vue";
import DetailGoodsInfo from "./ChildComs/DetailGoodsInfo.vue";
import DetailParamInfo from "./ChildComs/DetailParamInfo.vue";
import ShopList from "../../components/comment/ShopList/ShopList.vue";
import DetailCommentInfo from "./ChildComs/DetailCommentInfo.vue";
import DetailBottomBar from "./ChildComs/DetailBottomBar.vue";
import Backtop from '../../components/common/BackTop/Backtop.vue';

import {
  getDetail,
  Goods,
  Shop,
  GoodsParam,
  getRecommend,
} from "../../network/detail";

export default {
  name: "Detail",
  data() {
    return {
      topImages: [],
      goods: {},
      shop: {},
      detailInfo: {},
      paramInfo: {},
      commentInfo: {},
      recommends: [],
      display:false
    };
  },
  methods: {
    titleClick(index) {
      const detail_box = document.querySelector(".detail-container");
      switch (index) {
        case 0:
          document.querySelector(".detail-swiper").scrollIntoView({
            behavior: "smooth",
            block: "start", // 上边框与视窗顶部平齐。默认值
          });
          break;
        case 1:
          document.querySelector(".param-info").scrollIntoView({
            behavior: "smooth",
            block: "start", // 上边框与视窗顶部平齐。默认值
          });
          break;
        case 2:
          document.querySelector(".comment-info").scrollIntoView({
            behavior: "smooth",
            block: "start", // 上边框与视窗顶部平齐。默认值
          });
          break;
        case 3:
          document.querySelector(".shop-list").scrollIntoView({
            behavior: "smooth",
            block: "start", // 上边框与视窗顶部平齐。默认值
          });
          break;
      }
    },
    scrollto(e) {
      let top0 =
        document.querySelector(".detail-swiper").clientHeight +
        document.querySelector(".detail-base").clientHeight
        -44;
      let top1 =
        top0 +
        document.querySelector(".param-info").clientHeight +
        document.querySelector(".detail-goods").clientHeight +
        document.querySelector(".detail-shop").clientHeight;
      let top2 = top1 + document.querySelector(".comment-info").clientHeight;
      let top3 = top2 + document.querySelector(".shop-list").clientHeight;
      let scrolly = e.target.scrollTop;
      if (scrolly < top0) {
        this.$refs.detailnavbar.currentIndex = 0;
      } else if (scrolly > top0 && scrolly < top1) {
        this.$refs.detailnavbar.currentIndex = 1;
      } else if (scrolly > top1 && scrolly < top2) {
        this.$refs.detailnavbar.currentIndex = 2;
      } else if (scrolly > top2 && scrolly < top3) {
        this.$refs.detailnavbar.currentIndex = 3;
      }
      if(scrolly > 1000){
        this.display = true;
      }
    },
     BackTop(){
      const that = this.$refs['detail-container'];
      let timer = setInterval(() => {
        let ispeed = Math.floor(-that.scrollTop / 5);
        that.scrollTop  = that.scrollTop + ispeed
        if (that.scrollTop === 0) {
          clearInterval(timer);
        }
      }, 16)
     }
  },
  components: {
    DeatailNavbar,
    DetailSwiper,
    DetailBaseInfo,
    DetailShopInfo,
    DetailGoodsInfo,
    DetailParamInfo,
    DetailCommentInfo,
    ShopList,
    DetailBottomBar,
    Backtop,
  },
  created() {
    this.iid = this.$route.query.iid;
    // 2.根据iid请求详细数据
    getDetail(this.iid).then((res) => {
      // console.log(res);
      // 1.获取数据
      const data = res.result;
      // 2.取出顶部轮播图的数据
      this.topImages = data.itemInfo.topImages;
      this.goods = new Goods(
        data.itemInfo,
        data.columns,
        data.shopInfo.services
      );
      this.shop = new Shop(data.shopInfo);
      this.detailInfo = data.detailInfo;
      this.paramInfo = new GoodsParam(
        data.itemParams.info,
        data.itemParams.rule
      );
      if (data.rate.cRate !== 0) {
        this.commentInfo = data.rate.list[0];
      }
      getRecommend().then((res) => {
        this.recommends = res.data.list;
      });
    });
  },
};
</script>

<style scoped>
.detail-container {
  overflow-y: scroll;
  position: absolute;
  top: 44px;
  left: 0;
  right: 0;
  bottom: 0;
}
.detail {
  position: relative;
  width: 100vw;
  height: 100vh;
}
.detail-nav-bar {
  width: 100vw;
  background-color: #fff;
}
.bottom-bar {
  position: fixed;
  top: calc(100% - 49px);
  z-index: 5;
  width: 100%;
}
.backtop{
  position: fixed;
  bottom: 70px;
  right: 20px;
  z-index: 4;
}

</style>