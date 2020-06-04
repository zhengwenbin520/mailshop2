<template>
  <div id="home">
    <div class="sss">
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
    </div>
    <scroll class="content" ref="scr" :probe-type="3" @scroll="conentScroll" :pull-up-load="true" @pullingUp="leckend">
     <home-swiper :banners="banners"/>
     <recommend-view :recommend="recommend" /> 
     <feature-view />
     <table-contro :titles="titles" @tabclick="tabclick" ref="tableContro" />
     <goods-list :goods="showHome" />
    </scroll>
    <back-top @click.native="backClick" v-show="isShow"/>
  </div>
</template>


<script>
import HomeSwiper from './childComps/HomeSwiper'
import RecommendView from './childComps/RecommendView'
import FeatureView from './childComps/FeatureView'

import NavBar from "components/common/navbar/NavBar";
import tableContro from 'components/content/tableContro/TableContro'
import GoodsList from 'components/content/goods/GoodsList'
import Scroll from 'components/common/scroll/Scroll'
import BackTop from 'components/content/backTop/BackTop'


import { getHomeMultidata } from "network/home";
import { getHomeGoogs } from 'network/home'
import { debounce } from 'common/utils'

export default {
  name: "Home",
  components: {
    NavBar,
    HomeSwiper,
    RecommendView,
    FeatureView,
    tableContro,
    GoodsList,
    Scroll,
    BackTop
  },
  data() {
    return {
      isShow:false,
      banners: [],
      recommend: [],
      titles:['流行','新款','精选'],
      currentType:'pop',
      goods:{
        'pop':{page:0,list:[]},
        'new':{page:0,list:[]},
        'sell':{page:0,list:[]},
      }
    };
  },
  mounted() {
    this.getHomeMultidata();
    this.getHomeGoogs('pop');
    this.getHomeGoogs('new');
    this.getHomeGoogs('sell');

    const refresh = debounce(this.$refs.scr.refresh,50)


    console.log(this.$refs.tableContro)

    this.$bus.$on('itemImageLoad',()=>{
      //console.log('--------------------')
      refresh()
    })

  },
  computed:{
    showHome(){
      return this.goods[this.currentType].list
    }
  },
  methods:{
    /**
     * 监听事件
     */
      tabclick(index){
        switch(index){
          case 0:
            this.currentType = 'pop'
            break;
          case 1:
            this.currentType = 'new'
            break;
          case 2:
            this.currentType = 'sell'
            break

        }
      },

    backClick(){
      this.$refs.scr.scrollTo(0,0)
    },

    conentScroll(position){
      //console.log(position)
     this.isShow = (-position.y) > 1000
    },

    leckend(){
      //console.log(11)
      this.getHomeGoogs(this.currentType)
    },

   /*
     * 网络请求相关的
     */
    getHomeMultidata(){
      getHomeMultidata().then(res => {
      this.banners = res.data.banner.list;
      this.recommend = res.data.recommend.list
    });
    },
    getHomeGoogs(type){
      const page = this.goods[type].page+1
      getHomeGoogs(type,page).then(res => {
        this.goods[type].list.push(...res.data.list)
        this.goods[type].page +=1;

       // 完成上拉加载更多
       this.$refs.scr.finishPullUp()
    })
    }
  }
};
</script>

<style scoped>
#home{
  padding-top: 44px;
  height: 100vh;
  position: relative;
}
.home-nav {
  background-color: var(--color-tint);
  color: white;

  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  z-index: 9;
}
.content{
  /* height: 300px; */
  overflow: hidden;
  position: absolute;
  top: 44px;
  bottom: 49px;
  left: 0px;
  right: 0px;
}
</style>
