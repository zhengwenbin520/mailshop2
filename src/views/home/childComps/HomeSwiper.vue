<template>
  <div>
    <swiper>
      <swiper-item v-for="item in banners">
        <a :href="item.link">
          <img :src="item.image" class="home-nav" />
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
  }
};
</script>

<style scoped>

</style>