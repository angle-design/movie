<template>
  <div id="main">
    <Header title="喵喵影院"/>
    <div id="content">
      <div class="cinema_menu">
        <div class="city_switch">全城</div>
        <div class="brand_switch">品牌</div>
        <div class="feature_switch">特色</div>
      </div>
      <Clist/>
    </div>
    <Tab/>
  </div>
</template>

<script>
  import Header from '@/components/Header'
  import Tab from '@/components/TabBar'
  import Clist from '@/components/Clist'
  export default {
    name:'cinema',
    components:{
      Header,
      Tab,
      Clist
    }
  }
</script>

<style scoped>
.cinema_menu{
  width:100%;
  height:0.9rem;
  border-bottom:0.02rem solid #e6e6e6;
  display: flex;
  justify-content: space-around;
  align-items: center;
  background: #fff;
}
</style>
