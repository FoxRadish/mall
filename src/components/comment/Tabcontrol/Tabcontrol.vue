<template>
  <div class="box">
      <div v-for="(text,index) in title" @click="changeact(index)">
          <span :class="{actived:index === currentIndex}">{{text}}</span>
      </div>
  </div>
</template>

<script>
export default {
    props:{
        title:{
            type:Array,
            default:[]
        }
    },
    data () {
        return {
            currentIndex:0
        }
    },
    methods:{
        changeact(index){
           this.currentIndex = index;
           this.$emit('changetab',index);
        }
    }
}
</script>

<style scoped>
    .box{
        display: flex;
        position: sticky;
        top: 44px;
        z-index: 2;
        background-color: #fff;
    }
    .box div{
        text-align: center;
        flex: 1;
        height: 40px;
        line-height: 40px;
    }
    .box span{
        padding: 5px;
        padding-bottom: 8px;
    }
    .actived {
        color:var(--color-high-text);
        border-bottom: 3px solid var(--color-tint);
    }
</style>