<template>
  <div class="detail">
    <div>
      <derail-form />
    </div>
    <div>
      <derail-swiper :top-images="topImages" class="swiper-item" />
    </div>
  </div>
</template>

<script>
import DerailForm from "../detail/childComps/DerailForm";
import DerailSwiper from './childComps/DerailSwiper'

import { getdetail } from "network/detail";

export default {
  components: {
    DerailForm,
    DerailSwiper
  },
  data() {
    return {
      iid: null,
      topImages: []
    };
  },
  created() {
    this.iid = this.$route.params.iid;

    getdetail(this.iid).then(res => {
      console.log(res);
      this.topImages = res.result.itemInfo.topImages;
    });
  }
};
</script>

<style scoped>
</style>