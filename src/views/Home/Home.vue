<template>
  <div>
    <navbar class="nav-home"><div slot="center">购物车</div></navbar>
    <home-swiper
      :banners="banners"
    ></home-swiper>
    <recommend-view :recommends="recommends"></recommend-view>
  </div>
</template>

<script>
import Navbar from "components/common/Navbar/Navbar";
import { getHomeMultidata, getHomeGoods } from "network/home";
import HomeSwiper from "./ChildComponents/HomeSwiper.vue";
import RecommendView from './ChildComponents/RecommendView.vue';
export default {
  components: {
    Navbar,
    HomeSwiper,
    RecommendView,
  },
  data() {
    return {
      banners: [],
      recommends: [],
    };
  },
  methods: {
    getHomeMultidata() {
      getHomeMultidata().then((res) => {
        console.log(res);
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      });
    },
  },
   created() {
    this.getHomeMultidata();
  },
};
</script>

<style>
@import url(~assets/css/base.css);
.nav-home {
  background-color: var(--color-tint);
  color: white;

  /* 在使用浏览器原生滚动时，为了让导航不跟随一起滚动: */
  /* position: fixed;
    left: 0;
    right: 0;
    top: 0;
    z-index: 9; */
}
</style>