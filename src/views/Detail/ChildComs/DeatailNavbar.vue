<template>
  <div>
    <NavBar>
      <div class="back" @click="backClick" slot="left">
        <img src="~assets/img/common/back.svg" alt="" />
      </div>
        <div class="title" slot="center">
          <div
            v-for="(item, index) in titles"
            class="title-item"
            :class="{ active: index === currentIndex }"
            @click="titleClick(index)"
          >
            {{ item }}
          </div>
        </div>
    </NavBar>
  </div>
</template>

<script>
import NavBar from "components/common/Navbar/Navbar.vue";

export default {
  name: "DetailNavBar",
  components: {
    NavBar,
  },
  data() {
    return {
      titles: ["商品", "参数", "评论", "推荐"],
      currentIndex: 0,
    };
  },
  methods: {
    titleClick(index) {
      this.currentIndex = index;
      this.$emit("titleClick", index);
    },
    backClick() {
      this.$router.back();
    },
  },
};
</script>

<style scoped>
.title {
  display: flex;
  font-size: 13px;
}

.title-item {
  flex: 1;
}

.active {
  color: var(--color-high-text);
}

.back img {
  margin-top: 12px;
}
</style>
