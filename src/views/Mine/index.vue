<template>
  <div id="main">
    <Header title="我的电影"/>
    <div id="content">
      <Login/>
    </div>
    <Tab/>
  </div>
</template>

<script>
  import Header from '@/components/Header'
  import Tab from '@/components/TabBar'
  import Login from '@/components/Login'
  export default {
    name:'mine',
    components:{
      Header,
      Tab,
      Login
    }
  }
</script>

<style scoped>

</style>
