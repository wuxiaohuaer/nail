<template>
  <div class="wrap">
    <div class="pos"></div>
    <login></login>
    <register></register>
    <div class="index">
      <index-header></index-header>
      <div class="content">
        <index-swiper></index-swiper>
        <index-layout></index-layout>
        <index-global></index-global>
        <index-arch></index-arch>
      </div>
      <index-footer></index-footer>
    </div>
  </div>
</template>

<script>
import IndexHeader from './computed/head'
import IndexLayout from './computed/layout'
import IndexGlobal from './computed/global'
import IndexArch from './computed/arch'
import IndexFooter from './computed/footer'
import IndexSwiper from './computed/swiper'
import Login from './computed/login'
import Register from './computed/register'
export default {
  name:'Home',
  components:{
    IndexHeader,
    IndexLayout,
    IndexGlobal,
    IndexArch,
    IndexFooter,
    IndexSwiper,
    Login,
    Register
  }
}
</script>
<style lang="less">
  .wrap{
    width: 100%;
    overflow: hidden;
    position: relative;
    background: #3b3b3b;
    .pos{
      width: 100%;
      height: 346px;
      position: absolute;
      left: 1000px;
      top: 120px;
      background: url(../../assets/imgs/NAIL.png) no-repeat;
      background-size: 1100px 346px;
    }
    .index{
      width: 1500px;
      height: 100%;
      background: #fff;
      margin: 0 auto;
      .content{
        width: 100%;
      }
    }
  }
</style>

