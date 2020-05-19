<template>
  <div class="home-contro">
    <div
      v-for="(item, index) in titles"
      class="home-contro-title"
      :class="{active:index===countIndex}"
      @click="tableCont(index)"
    >
      <span>{{ item }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "TableContro",
  props: {
    titles: {
      type: Array,
      default() {
        return [];
      }
    }
  },
  data() {
    return {
      countIndex: 0
    };
  },
  methods:{
      tableCont(index){
          this.countIndex = index
      }
  }
};
</script>

<style scoped>
.home-contro {
  display: flex;
  text-align: center;
  height: 40px;
  line-height: 40px;
  font-size: 15px;
  background-color: white;
}
.home-contro-title {
  flex: 1;
}
.home-contro-title span{
    padding: 5px;
}
.active{
    color: var(--color-high-text);
}
.active span{
    border-bottom: 3px solid var(--color-tint);
}
</style>