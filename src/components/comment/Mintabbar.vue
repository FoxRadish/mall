<template>
   <div class="tabbar">
      <tabbar-item path="/home" > <!--act_text_color="red" 可以改变显示字体的颜色-->
          <img src="~@img/tabbar/home.svg" slot="item-icon">
          <img src="~@img/tabbar/home_active.svg" slot="item-icon-active">
          <div slot="itme-text">首页</div>
      </tabbar-item>
      <tabbar-item path="/category">
          <img src="~@img/tabbar/category.svg" slot="item-icon">
          <img src="~@img/tabbar/category_active.svg" slot="item-icon-active">
          <div slot="itme-text">分类</div>
      </tabbar-item>
      <tabbar-item path="/cart">
          <img src="~@img/tabbar/shopcart.svg" slot="item-icon">
          <img src="~@img/tabbar/shopcart_active.svg" slot="item-icon-active">
          <div slot="itme-text">购物车</div>
      </tabbar-item>
      <tabbar-item path="/mine">
          <img src="~@img/tabbar/mine.svg" slot="item-icon">
          <img src="~@img/tabbar/mine_active.svg" slot="item-icon-active">
          <div slot="itme-text">我的</div>
      </tabbar-item>
  </div>
</template>

<script>
import TabbarItem from '../common/tabbar/Tabbar_item.vue'
export default {
    components: {
        tabbarItem:TabbarItem
    },
}
</script>

<style scoped>
.tabbar{
    display: flex;
    position: fixed;
    bottom: 0;
    height: 50px;
    width: 100%;
    background-color: #f4f4f4;
    box-shadow: 0px -1px 3px 1px rgba(0, 0, 0, .2);
}
</style>