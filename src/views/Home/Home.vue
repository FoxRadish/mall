<template>
  <div @scroll="showTop" class="home-container" ref="container">
    <navbar class="nav-home"><div slot="center">购物车</div></navbar>
      <home-swiper :banners="banners"></home-swiper>
      <recommend-view :recommends="recommends"></recommend-view>
      <feature-view></feature-view>
      <tabcontrol :title="['流行', '新款', '精选']" @changetab="changetab" />
      <shop-list :shop="shops[currentType].list" />
    <backtop class="backtop" @click.native="BackTop" v-show="display"/>
  </div>
</template>

<script>
//该页面定制的组件
import HomeSwiper from "./ChildComponents/HomeSwiper.vue";
import RecommendView from "./ChildComponents/RecommendView.vue";
import FeatureView from "./ChildComponents/FeatureView.vue";
//可以公用的组件
import Navbar from "components/common/Navbar/Navbar";
import ShopList from "components/comment/ShopList/ShopList.vue";
import Tabcontrol from "components/comment/Tabcontrol/Tabcontrol.vue";
import Backtop from 'components/common/BackTop/Backtop.vue';
// 功能模块
import { getHomeMultidata, getHomeGoods } from "network/home";



export default {
  components: {
    Navbar,
    HomeSwiper,
    RecommendView,
    FeatureView,
    Tabcontrol,
    ShopList,
    Backtop,
  },
  data() {
    return {
      banners: [],
      recommends: [],
      shops: {
        pop: { page: 0, list: [] },
        new: { page: 0, list: [] },
        sell: { page: 0, list: [] },
      },
      currentType: "pop",
      display:false,
      scrollY:0,
    };
  },
  methods: {
    /*
     **网络请求相关的数据
     */
    getHomeMultidata() {
      getHomeMultidata().then((res) => {
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      });
    },
    getHomeGoods(type) {
      const page = this.shops[type].page + 1;
      getHomeGoods(type,page).then((res) => {
        this.shops[type].list.push(...res.data.list);
        this.shops[type].page += 1;
      });
      
    },
    /*
     **事件监听相关内容
     */
    changetab(index) {
      if (index === 0) this.currentType = "pop";
      else if (index === 1) this.currentType = "new";
      else if (index === 2) this.currentType = "sell";
    },
    BackTop(){
      const that = this.$refs.container;
      let timer = setInterval(() => {
        let ispeed = Math.floor(-that.scrollTop / 5);
        that.scrollTop  = that.scrollTop + ispeed
        if (that.scrollTop === 0) {
          clearInterval(timer);
        }
      }, 16)

    },
    showTop(e){
     if(e.target.scrollTop > 900){
       this.display = true;
     }else{
       this.display = false;
     };
     if(e.target.clientHeight + e.target.scrollTop == e.target.scrollHeight){
       this.getHomeGoods(this.currentType);
     }
    }
    
  },

  created() {
    this.getHomeMultidata();

    this.getHomeGoods("pop");
    this.getHomeGoods("new");
    this.getHomeGoods("sell");
  },
  activated(){
    this.$refs.container.scrollTop = this.scrollY;
  },
  beforeRouteLeave(to, from, next){
    if(to.path == '/detail'){
      this.scrollY = this.$refs.container.scrollTop; 
    }
    next();
  }
};
</script>

<style scoped>
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
.home-container{
  height: calc(100vh - 49px);
  overflow-y: scroll;
}
.backtop{
  position: fixed;
  bottom: 70px;
  right: 20px;
}

</style>