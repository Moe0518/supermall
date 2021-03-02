<template>
  <scroller ref="myscroller" :on-refresh="refresh" :on-infinite="infinite" :noDataText="noDataText">
    <slot></slot>
  </scroller>
</template>

<script>
  import Vue from 'vue'
  import VueScroller from 'vue-scroller'

  Vue.use(VueScroller)
    export default {
      name: "Scroll",
      data(){
        return{
          scroll:null,
          noDataText:"--我也是有底线的--",
        }
      },
      props:{
        myData: {
          type: Object,
          default() {
            return {}
          }
        }
      },
      methods:{

        infinite(){
          console.log('infinite')
          setTimeout(()=>{
            if (this.myData.length >= 20) {
              this.$refs.myscroller.finishInfinite(true);
            }else{
              this.$refs.myscroller.finishInfinite(false);
            }
            //this.$refs.myscroller.resize();//已弃用，
            //this.myData.push(this.myData[1]);
          }, 500)
        },
        refresh(){
          console.log('refresh')
          setTimeout(()=>{
            this.$refs.myscroller.finishPullToRefresh()
          }, 500)
        },
        scrollTo(x, y, z) {
          this.$refs.myscroller.scrollTo(x, y, z)
        }
        // goodsAll(){
        //   this.status = 'all'
        //   this.page = 0
        //   this.all_page = 1
        //   this.$refs.myscroller.finishInfinite(false);
        //   //this.orderList = []
        // },
      }
    }
</script>

<style scoped>

</style>
