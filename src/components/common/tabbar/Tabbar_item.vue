<template>
  <div class="tabbar_item" @click="changeRouter">
      <div v-if="active">
        <slot name="item-icon"></slot>
      </div>
      <div v-else>
        <slot name="item-icon-active"></slot>
      </div>
    <div :style="active_text_color">
        <slot name="itme-text"></slot>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    changeRouter(){
      this.$router.replace(this.path);
    }
  },
  props:{
    path: String,
    act_text_color:{
      type:String,
      default: '#777bce'
    }
  },
  computed: {
    active(){
       return this.$route.path.indexOf(this.path);
    },
    active_text_color(){
      return !this.active? {color:this.act_text_color}: {}
    }
  }
};
</script>

<style>
 .tabbar_item {
     flex: 1;
     text-align: center;
 }
 .tabbar_item img{
     width: 24px;
     height: 24px;
 }
</style>