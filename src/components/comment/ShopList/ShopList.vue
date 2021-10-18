<template>
  <div class="shop">
    <shop-list-item v-for="item in shop" :shop-item="item" />
  </div>
</template>

<script>
import ShopListItem from './ShopListItem.vue';

  export default {
    name: "ShopList",
    components:{
      ShopListItem
    },
    props: {
      shop: {
        type: Array,
        default() {
          return []
        }
      }
    },
  };
</script>

<style scoped>
  .shop {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;

    padding: 2px;
  }
</style>
