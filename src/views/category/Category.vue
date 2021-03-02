<template>
  <div class="content">
    <scroll :myData="myData" >
      <h2>分类</h2>
      <ul>
        <li v-for="(item,index) in myData" :key="index">{{item}}</li>
      </ul>
    </scroll>
  </div>
</template>

<script>

  import Scroll from 'components/common/scroller/Scroll'

  export default {
    name: "Category",
    data(){
      return{
        myData:["helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword","helloword"],
        status:'all',
        page:0,
        all_page:1,
      }
    },

    components: {
     Scroll,
    },
    methods: {


    },

    }
</script>

<style scoped>
  .content {
    position: absolute;
    top: 44px;
    bottom: 49px;
    left: 0;
    right: 0;
  }
</style>
