<template>
  <div id="home">
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
    <home-swiper :banners="banners"></home-swiper>
    <recommentd-view :recommends="recommends"></recommentd-view>
  </div>
</template>
<script>
import NavBar from "@/components/common/navbar/NavBar.vue";
import HomeSwiper from './HomeSwiper.vue';
import RecommentdView from './childComps/RecommentdView.vue';



import {getHomeMultidata} from "@/network/home";

export default {
  name: "Home",
  components: {
    NavBar,
    HomeSwiper,
    RecommentdView,
  },
  data() {
    return {
      //定义变量接受服务器数据
      banners: [],
      recommends: [],
    };
  },
  created() {
    //1.请求多个数据
    getHomeMultidata().then((res) => {
      console.log(res);
      this.banners = res.data.banner.list;
      this.recommends = res.data.recommend.list;
    });
  },
};
</script>
<style>
.home-nav {
  background-color: var(--color-tint);
  color: white;
}
</style>