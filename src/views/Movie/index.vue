<template>
  <div id="main">
    <Header title="喵喵电影"/>
    <div id="content">
      <div class="movie_menu">
        <router-link tag="div" to="/movie/city" class="city_name">
          <span>{{$store.state.city.nm}}</span>
        </router-link>
        <div class="hot_switch">
          <router-link tag="div" to="/movie/nowplaying" class="hot_item">正在热映</router-link>
          <router-link tag="div" to="/movie/comming" class="hot_item">即将上映</router-link>
        </div>
        <router-link tag="div" to="/movie/search" class="search_entry">
          搜索
        </router-link>
      </div>
      <keep-alive>
        <router-view/>
      </keep-alive>
    </div>
    <Tab/>
    <router-view name="detail" />
  </div>
</template>

<script>
  import Header from '@/components/Header'
  import Tab from '@/components/TabBar'
  import {messagebox} from '@/components/js'

  export default {
    name: 'movie',
    components: {
      Header,
      Tab
    },
    mounted(){
      setTimeout(()=>{
        this.axios.get('/api/getLocation').then(res=>{
          var msg=res.data.msg;
          if(msg==='ok'){
            var nm=res.data.data.nm;
            var id=res.data.data.id;
            if(this.$store.state.city.id == id){return;}
            messagebox({
              title: '定位',
              content:nm,
              cancle:'取消',
              ok:'切换定位',
              handleCancel(){
                console.log(1)
              },
              handleOk(){
                window.localStorage.setItem('nowNm',nm)
                window.localStorage.setItem('nowId',id)
                window.location.reload()
              }
            })
          }
        })
      },3000)


    }
  }
</script>

<style scoped lang="less">
  #content {
    flex: 1;
    overflow: auto;
    margin-bottom: 1rem;
    position: relative;
    display: flex;
    flex-direction: column;
    .movie_menu {
      width: 100%;
      height: 0.9rem;
      border-bottom: 0.02rem solid #ccc;
      display: flex;
      justify-content: space-between;
      .city_name {
        margin-left: 0.4rem;
        height: 100%;
        line-height: 0.9rem;
        box-sizing: border-box;
        &.active {
          color: #ef4238;
          border-bottom: 0.04rem #ef4238 solid;
        }
        &.router-link-active {
          color: #ef4238;
          border-bottom: 0.04rem #ef4238 solid;
        }
      }
      .hot_switch {
        display: flex;
        height: 100%;
        line-height: 0.9rem;
        .hot_item {
          font-size: 0.3rem;
          color: #666;
          width: 1.6rem;
          text-align: center;
          margin: 0 0.24rem;
          font-weight: 700;
          &.active {
            color: #ef4238;
            border-bottom: 0.04rem #ef4238 solid;
          }
          &.router-link-active {
            color: #ef4238;
            border-bottom: 0.04rem #ef4238 solid;
          }
        }
      }
      .search_entry {
        margin-right: 0.4rem;
        height: 100%;
        line-height: 0.9rem;
        &.active {
          color: #ef4238;
          border-bottom: 0.04rem #ef4238 solid;
        }
        &.router-link-active {
          color: #ef4238;
          border-bottom: 0.04rem #ef4238 solid;
        }
      }
    }
  }
</style>
