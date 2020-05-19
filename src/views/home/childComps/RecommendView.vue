<template>
  <div class="recommend">
    <div v-for="item in recommend" class="recommend-view">
      <a :href="item.link">
        <img :src="item.image" />
        <div>{{ item.title }}</div>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    recommend: {
      type: Array,
      default() {
        return [];
      }
    }
  }
};
</script>

<style scoped>
 .recommend{
     display:flex;
     text-align: center;
     width: 100%;
     padding: 10px 0px 20px;
     font-size: 15px;
     border-bottom:8px solid #eee;
 }
 .recommend-view{
     flex:1
 }
 .recommend-view img {
     
     width:70px;
     height:70px;
     margin-bottom: 3px;
 }
</style>