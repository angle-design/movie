<template>
    <header id="header">
      <slot></slot> <h1>{{title}}</h1>
    </header>
</template>

<script>
    export default {
      name: "Header",
      props:{
        title:{
          type: String,
          default:'喵喵电影'
        }
      }
    }
</script>

<style scoped lang="less">
#header{
  width:100%;
  height:1rem;
  background:#e54847;
  color:#fff;
  position: relative;
  text-align: center;
  line-height: 1rem;
  h1{
    font-size:0.36rem;
  }
}
</style>
