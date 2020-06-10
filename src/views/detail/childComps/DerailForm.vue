<template>
  <div>
    <navbar>
      <div slot="left">
          <div class="back">
              <img src="~assets/img/common/back.svg" alt=""  @click="backclick"/>
          </div>
      </div>
      <div slot="center" class="center">
        <div
          v-for="(item,index) in titles"
          class="conter-title"
          :class="{active:index === currterindex}"
          @click="titleClick(index)"
        >{{ item }}</div>
      </div>
    </navbar>
  </div>
</template>

<script>
import Navbar from "components/common/navbar/NavBar";
export default {
  components: {
    Navbar
  },
  data() {
    return {
      currterindex: 0,
      titles: ["商品", "参数", "评论", "推荐"]
    };
  },
  methods:{
      titleClick(index){
        this.currterindex =  index 
      },
      backclick(){
        this.$router.go(-1)  
      }
  }
};
</script>

<style scoped>
.center {
  display: flex;
  font-size: 13px;
}
.conter-title {
  flex: 1;
}
.active {
  color: var(--color-high-text);
}
.back img{
    margin-top: 12px;
    margin-right: 15px;
}
</style>