<template>
  <div class="wrapper" ref="query">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BSscroll from "better-scroll";
export default {
  props: {
    probeType: {
      type: Number,
      default: 0
    },
    pullUpLoad: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      scroll: null
    };
  },

  mounted() {
    // 1. 创建scroll对象
    this.scroll = new BSscroll(this.$refs.query, {
      probeType: this.probeType,
      pullUpLoad: this.pullUpLoad,
      click: true
    });

    // 2. 子传父 滚动消失和隐藏时间
    if (this.probeType == 2 || this.probeType == 3) {
      this.scroll.on("scroll", postition => {
        //console.log(postition)\
        this.$emit("scroll", postition);
      });
    }
    if (this.pullUpLoad) {
      this.scroll.on('pullingUp',()=>{
        console.log('直接拉到底部')
        this.$emit('pullingUp')
      })
    }
  },

  methods: {
    scrollTo(x, y, time = 300) {
      this.scroll && this.scroll.scrollTo(x, y, time);
    },
    finishPullUp() {
      this.scroll.finishPullUp();
    },
    refresh() {
      console.log(11111);
      this.scroll && this.scroll.refresh();
    }
  }
};
</script>

<style>
</style>