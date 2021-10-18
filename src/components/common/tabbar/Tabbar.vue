<template>
  <div>
    <keep-alive exclude="Detail">
      <router-view />
    </keep-alive>
    <mintabbar />
  </div>
</template>

<script>
import MintabbarVue from "../../comment/Mintabbar.vue";

export default {
  components: {
    mintabbar: MintabbarVue,
  },
};
</script>

<style>
</style>