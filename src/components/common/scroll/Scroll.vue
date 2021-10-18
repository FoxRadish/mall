<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
  import BScroll from 'better-scroll'

  export default {
    name: "Scroll",
    data() {
      return {
        scroll: null
      }
    },
    mounted() {
      // 1.创建BScroll对象
      setTimeout(() => {
        this.scroll = new BScroll(this.$refs.wrapper, {
        click: true,
        probeType: 3,
        pullUpLoad: true,
      });
      this.scroll.on('scroll',(position) => {
        console.log(position.y);
        this.$emit('topshow',position.y);
        
      })
      }, 2000);
    },
    methods:{
      scrollTo(x,y,time = 300){
        this.scroll.scrollTo(x,y,time)
      }
    }
  }
</script>

<style scoped>
 
</style>