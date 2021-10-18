<template>
  <div class="shop-item" @click="itemClick">
    <img :src="showImage" alt="">
    <div class="shop-info">
      <p> {{shopItem.title}} </p>
      <span class="price"> ￥{{shopItem.price}} </span>
      <span class="collect"> {{shopItem.cfav}} </span>
    </div>
  </div>
</template>

<script>
  export default {
    name: "ShopListItem",
    props: {
      shopItem: {
        type: Object,
        default() {
          return {}
        }
      }
    },
    computed: {
      showImage() {
        return this.shopItem.image || this.shopItem.show.img
      }
    },
    methods: {
      itemClick(){
        this.$router.push(`/detail?iid=${this.shopItem.iid}`);
      }
    }
  }
</script>

<style scoped>
  .shop-item {
    padding-bottom: 40px;
    position: relative;

    width: 48%;
  }

  .shop-item img {
    width: 100%;
    border-radius: 5px;
  }

  .shop-info {
    font-size: 12px;
    position: absolute;
    bottom: 5px;
    left: 0;
    right: 0;
    overflow: hidden;
    text-align: center;
  }

  .shop-info p {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    margin-bottom: 3px;
  }

  .shop-info .price {
    color: var(--color-high-text);
    margin-right: 20px;
  }

  .shop-info .collect {
    position: relative;
  }

  .shop-info .collect::before {
    content: '';
    position: absolute;
    left: -15px;
    top: -1px;
    width: 14px;
    height: 14px;
    background: url("~assets/img/common/collect.svg") 0 0/14px 14px;
  }
</style>
