<template>
    <div id="home">
      <nav-bar class="home-nav"><div slot="center">购物车</div></nav-bar>
      <home-swiper :banners="banners"/>
      <recommend-view :recommends="recommends"/>
      <feature-view></feature-view>
      <tab-control class="tab-control"
                   :titles = "['流行','新款','精选']"
                   @tabClick="tabClick" />
      <goods-list :goods = "showGoods"/>
    </div>
</template>

<script>
  import NavBar from 'components/common/navbar/NavBar'
  import HomeSwiper from './childComps/HomeSwiper'
  import RecommendView from './childComps/RecommendView'
  import FeatureView from  './childComps/FeatureView'
  import GoodsList from  'components/content/goods/GoodsList'

  import TabControl from 'components/content/tabControl/TabControl'

  import {getMultiData,getProductData} from 'network/home'
    export default {
      name: "Home",
      components:{
        NavBar,
        HomeSwiper,
        RecommendView,
        FeatureView,
        TabControl,
        GoodsList,
      },
      created(){
        this.getMultiData(),
          this.getProductData('pop'),
          this.getProductData('new'),
          this.getProductData('sell')
      },
      data(){
        return{
          banners:[],
          recommends:[],
          goods:{
            'pop':{page:0,list:[]},
            'new':{page:0,list:[]},
            'sell':{page:0,list:[]},
          },
          currentType:'pop'
        }
      },
      computed:{
        showGoods(){
          return this.goods[this.currentType].list
        }
      },
      methods: {
        tabClick(index){
          switch (index) {
            case 0:
              this.currentType = 'pop';
              break;
            case 1:
              this.currentType = 'new';
              break;
            case 2:
              this.currentType = 'sell';
              break;
          }
        },

        getMultiData() {
          getMultiData().then(res => {
            console.log(res)
            //this.result = res;
            this.banners = res.data.banner.list;
            this.recommends = res.data.recommend.list;
          })
        },
        getProductData(type){
          const page = this.goods[type].page + 1;
          getProductData(type,page).then(res => {
            console.log(res)
            this.goods[type].list.push(...res.data.list)
            this.goods[type].page += 1;
          })
        }
      },
    }
</script>

<style scoped>
  #home {
    height: 100vh;
    position: relative;
  }

  .home-nav {
    background-color: var(--color-tint);
    color: #fff;
    position: relative;
    z-index: 9;
  }

  .tab-control {
    /*position: relative;*/
    z-index: 9;
    position: sticky;
    top: 44px;
  }

  .content {
    position: absolute;
    top: 44px;
    bottom: 49px;
    left: 0;
    right: 0;
  }

</style>
