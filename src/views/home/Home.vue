<template>
  <div id="home">
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
     <home-swiper :banners="banners"/>
     <recommend-view :recommend="recommend" /> 
     <feature-view />
     <table-contro class="table-con" :titles="titles" />
     <ul>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
       <li>列表</li>
     </ul>
  </div>
</template>


<script>
import HomeSwiper from './childComps/HomeSwiper'
import RecommendView from './childComps/RecommendView'
import FeatureView from './childComps/FeatureView'

import NavBar from "components/common/navbar/NavBar";
import TableContro from 'components/content/tableContro/TableContro'

import { getHomeMultidata } from "network/home";
import { getHomeGoogs } from 'network/home'

export default {
  name: "Home",
  components: {
    NavBar,
    HomeSwiper,
    RecommendView,
    FeatureView,
    TableContro
  },
  data() {
    return {
      banners: [],
      recommend: [],
      titles:['流行','新款','精选'],
      goods:{
        'pop':{page:0,list:[]},
        'new':{page:0,list:[]},
        'sell':{page:0,list:[]},
      }
    };
  },
  mounted() {
    this.getHomeMultidata();
    getHomeGoogs().then(res => {

    })
  },
  methods:{
    getHomeMultidata(){
      getHomeMultidata().then(res => {
      this.banners = res.data.banner.list;
      this.recommend = res.data.recommend.list
    });
    }
  }
};
</script>

<style scoped>
.home-nav {
  background-color: var(--color-tint);
  color: white;

  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  z-index: 9;
}
.table-con{
  position: sticky;
  top:44px;
}
</style>
