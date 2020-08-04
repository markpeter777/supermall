<template>
  <div id="home">
    <nav-bar class="home-nav"><div slot="center">购物节</div></nav-bar>
    <scroll class="content">
      <home-swiper :banners="banners" />
      <home-recommend-view :recommends = "recommends"/>
      <home-feature-view />
      <tab-control class="tab-control" :titles="['流行','新款','精选']" @tabClick="tabClick" />
      <goods-list :goods="showGoods" />
    </scroll>
    <ul>
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
      <li>5</li>
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
      <li>5</li>
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
      <li>5</li>
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
      <li>5</li>
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
      <li>5</li>
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
      <li>5</li>
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
      <li>5</li>
    </ul>
  </div>
</template>

<script>
 import NavBar from 'components/common/navbar/NavBar'
 import HomeSwiper from './childComps/HomeSwiper'
 import HomeRecommendView from './childComps/HomeRecommendView'
 import HomeFeatureView from './childComps/HomeFeatureView'
 import TabControl from 'components/content/tabControl/TabControl'
 import GoodsList from 'components/content/goods/GoodsList'
 import Scroll from 'components/common/scroll/Scroll'
 import {getHomeMultidata,getHomeGoods} from 'network/home'

  export default {
    name: "Home",
    components:{
      NavBar,
      HomeSwiper,
      HomeRecommendView,
      HomeFeatureView,
      TabControl,
      GoodsList,
      Scroll
    },
    data() {
      return{
        banners : [],
        recommends: [],
        goods:{
          'pop':{page:0, list:[]},
          'new':{page:0, list:[]},
          'sell':{page:0, list:[]},
        },
        currentType:'pop'
      }
    },

    computed: {
      showGoods(){
        return this.goods[this.currentType].list
      }
    },
    
    created() {
      //1.请求首页的多个数据
      this.getHomeMultidata();
      //2.请求首页的商品数据
      this.getHomeGoods('pop');
      this.getHomeGoods('new');
      this.getHomeGoods('sell');
    },
    methods: {
      /*
        *事件监听相关的代码
      */
     tabClick(index){
       switch(index){
         case 0:
           this.currentType = 'pop'
           break
          case 1:
           this.currentType = 'new'
           break
          case 2:
           this.currentType = 'sell'
           break
       }
     },

      /*
       *网络请求相关的代码 
      */
      getHomeMultidata(){
        getHomeMultidata().then(res=>{
          this.banners = res.data.banner.list;
          this.recommends = res.data.recommend.list
        });
      },

      getHomeGoods(type){
        const page = this.goods[type].page+1;
        getHomeGoods(type,page).then(res=>{
          this.goods[type].list.push(...(res.data.list))
          this.goods[type].page+=1
        });
      }
    },
  }
</script>

<style scoped>
#home{
  padding-top: 44px;
  position: relative;
}
.home-nav{
  background-color:var(--color-tint);
  color: #fff;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 5;
}
.tab-control{
  position: sticky;
  background-color: #fff;
  top:44px;
  z-index: 5;
}
/* 方案一 利用定位做全屏 */
.content{
  overflow: hidden;
  position: absolute;
  top:44px;
  bottom: 49px;
  left: 0;
  right: 0;
  background-color: #fff;
}
</style>
