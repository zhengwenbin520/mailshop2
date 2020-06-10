<template>
  <div>
    <swiper>
      <swiper-item v-for="item in banners">
        <a :href="item.link">
          <img :src="item.image" class="home-nav" @load="loadImage" />
        </a>
      </swiper-item>
    </swiper>
  </div>
</template>

<script>
import { Swiper, SwiperItem } from "components/common/swiper";
// 这不是踢了了吗
export default {
  name: "HomeSwiper",
  props:{
      banners:{
          type:Array,
          default(){
              return[]
          }
      }
  },
  components: {
    Swiper,
    SwiperItem
  },
  data(){
    return{
      isLoad:false
    }
  },
  methods:{
    loadImage(){
      if (!this.isLoad) {
        this.$emit('swiper')
        this.isLoad = true
      }
      
    }
  }
};
</script>

<style scoped>

</style>