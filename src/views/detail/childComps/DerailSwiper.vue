<template>
  <div>
      <swiper class="swiper">
          <swiper-item v-for="item in topImages" >
              <img :src="item" alt="" />
          </swiper-item>
      </swiper>
  </div>
</template>

<script>
import { Swiper, SwiperItem } from "components/common/swiper/index";
export default {
  components: {
    Swiper,
    SwiperItem
  },
  props: {
    topImages: {
      type: Array,
      default() {
        return [];
      }
    }
  }
};
</script>

<style scoped>
.swiper{
    height: 300px;
}
</style>