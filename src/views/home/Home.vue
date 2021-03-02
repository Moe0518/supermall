<template>
    <div id="home">
      <nav-bar class="home-nav"><div slot="center">购物车</div></nav-bar>
      <scroll class="content" ref="scroll" :mayData="showGoods" >
        <home-swiper :banners="banners"/>
        <recommend-view :recommends="recommends"/>
        <feature-view></feature-view>
        <tab-control class="tab-control"
                     :titles = "['流行','新款','精选']"
                     @tabClick="tabClick" />
        <goods-list :goods = "showGoods"/>
      </scroll>
      <back-top @click.native="backClick"/>
    </div>
</template>

<script>
  import HomeSwiper from './childComps/HomeSwiper'
  import RecommendView from './childComps/RecommendView'
  import FeatureView from  './childComps/FeatureView'

  import GoodsList from  'components/content/goods/GoodsList'
  import NavBar from 'components/common/navbar/NavBar'
  import TabControl from 'components/content/tabControl/TabControl'
  import Scroll from 'components/common/scroller/Scroll'
  import BackTop from 'components/content/backTop/BackTop'

  import { getMultiData } from 'network/home'
    export default {
      name: "Home",
      components:{
        Scroll,
        NavBar,
        HomeSwiper,
        RecommendView,
        FeatureView,
        TabControl,
        GoodsList,
        BackTop,
      },
      created(){
        this.getMultiData(),
        //this.getProductData('pop'),
        //this.getProductData('new'),
        //this.getProductData('sell'),
        this.popList()
      },
      data(){
        return{
          banners:[],
          recommends:[],
          goods:{
            'pop':{ page:4 , list:[] },
            'new':{ page:2 , list:[] },
            'sell':{ page:3 , list:[] },
          },
          currentType:'pop',
        }
      },
      computed:{
        showGoods(){
          return this.goods[this.currentType].list;
        },

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
          this.popList()
        },
        backClick(){
          this.$refs.scroll.scrollTo( 0, 0, true)
        },

        getMultiData() {
          getMultiData().then(res => {
            //console.log(res)
            //this.result = res;
            this.banners = res.data.banner.list;
            this.recommends = res.data.recommend.list;
          })
        },
        popList(){
          let list = this.goods[this.currentType].list;
          let page = this.goods[this.currentType].page;
          for( let i=0; i < page*10; i++ ){
            let listItem = {};
            listItem.title = i +' 衬衫女韩版长袖显瘦雪纺春季新款';
            listItem.price = 132;
            listItem.cfav = i + 5;
            listItem.image = require('./../../assets/img/goods/shirt.jpg');
            list.push( listItem);
          }
        }
        // getProductData(type){
        //   const page = this.goods[type].page + 1;
        //   this.goods[type].list.push(...res.data.list)
        //   this.goods[type].page += 1;
        // }
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
    /*position: relative;
    z-index: 9;*/
    position: sticky;
    top: 44px;
  }

  .content {
    position: absolute;
    top: 44px;
    bottom: 49px;
    left: 0;
    right: 0;
    overflow: scroll;
  }

</style>
