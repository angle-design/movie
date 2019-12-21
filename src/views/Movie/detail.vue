<template>
  <div class="detailcontent slide-router-active">
    <Header title="影片详情">
      <span class="return" @touchstart="handleToBack">返回</span>
    </Header>
  </div>
</template>

<script>
    import Header from '@/components/Header'
    export default {
      name: "detail",
      components:{
        Header
      },
      props:['movieid'],
      methods:{
        handleToBack(){
          this.$router.back()
        }
      },
      mounted(){
        console.log(this.movieid)
      }
    }
</script>

<style scoped>
.detailcontent{
  position: absolute;
  top:0;
  left:0;
  z-index:100;
  width:100%;
  min-height:100%;
  background:#fff;
}
  .return{
    position: absolute;
    top:0;
    left:0.2rem;
  }
  .slide-router-active{
    animation:0.4s slidemove;
  }
  @keyframes  slidemove{
    0%{transform: translateX(100%)}
    100%{transform: translateX(0)}
  }
</style>
