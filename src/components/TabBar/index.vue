<template>
  <footer id="footer">
    <ul>
      <router-link tag="li" to="/movie">
        电影
      </router-link>
      <router-link  tag="li" to="/cinema">
        影院
      </router-link>
      <router-link  tag="li" to="/mine">
        我的
      </router-link>
    </ul>
  </footer>
</template>

<script>
  export default {
    name:'Tab'
  }
</script>

<style scoped lang="less">
#footer{
  width:100%;
  height:1rem;
  background: #fff;
  border-top:0.04rem solid #ccc;
  position: fixed;
  bottom:0;
  left:0;
  color:#333;
  line-height:1rem;
  font-size:0.32rem;
  ul{
    display: flex;
    text-align: center;
    align-items: center;
    li{
      flex:1;
      &.active{
        color:#ff6000;
      }
      &.router-link-active{
        color:#ff6000;
      }
    }
  }
}
</style>
