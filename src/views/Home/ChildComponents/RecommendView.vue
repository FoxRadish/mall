<template>
  <div class="recommend_box">
      <div v-for="(item,index) in recommends" :key="index" class="msg_box">
          <a :href="item.link">
              <img :src="item.image" alt="" srcset="">
              <div>{{item.title}}</div>
          </a>
      </div>
  </div>
</template>

<script>
export default {
 name:'RecomendView',
 props:{
     recommends:{
         type:Array,
         default:[]
     }
 }
}
</script>

<style scoped>
    .recommend_box{
        display: flex;
        text-align: center;
        font-size: 12px;
        border-bottom: 10px solid #eee;
    }
    .msg_box{
        margin: 15px 0 30px ;
        flex: 1;
    }
    .msg_box img{
        width: 65px;
        height: 65px;
    }
    .msg_box div {
        margin-top: 10px;
    }
</style>