<template>
  <div class="city_body">
    <div class="city_list">
        <div class="city_hot">
          <h2>热门城市</h2>
          <ul>
            <li>上海</li>
            <li>上海</li>
            <li>上海</li>
            <li>上海</li>
          </ul>
        </div>
      <div class="city_sort">
        <div>
          <h2>A</h2>
          <ul>
            <li>阿拉圣灯</li>
            <li>安庆</li>
          </ul>
        </div>
        <div>
          <h2>B</h2>
          <ul>
            <li>阿拉圣灯</li>
            <li>安庆</li>
          </ul>
        </div>
      </div>
    </div>
      <div class="city_index">
        <ul>
          <li>A</li>
          <li>B</li>
        </ul>
      </div>
  </div>

</template>

<script>
    export default {
        name: "city"
    }
</script>

<style scoped lang="less">
  .city_body{
    margin-top:0.9rem;
    display: flex;
    width:100%;
    position: absolute;
    top:0;
    bottom:0;
    .city_list{
      flex:1;
      overflow: auto;
      background:#fff5f0;
      &::-webkit-scrollbar{
        background-color:transparent;
        width:0;
      }
      .city_hot{
        margin-top:0.4rem;
        h2{
          padding-left:0.3rem;
          line-height:0.6rem;
          font-size:0.28rem;
          background:#f0f0f0;
          font-weight:normal;
        }
        ul{
          overflow: auto;
          li{
            float: left;
            background:#fff;
            width:29%;
            height:0.66rem;
            margin-top:0.3rem;
            margin-left:3%;
            padding:0.08rem;
            border:0.02rem solid #c6c6c6;
          }
        }
      }
      .city_sort{
        div{
          margin-top:0.4rem;
          h2{
            padding-left:0.3rem;
            line-height:0.6rem;
            font-size:0.28rem;
            background:#f0f0f0;
            font-weight:normal;
          }
          ul{
          padding-left:0.2rem;
            margin-top:0.2rem;
            li{
              line-height:0.6rem;
            }
          }
        }
      }
    }
    .city_index{
      width:0.4rem;
      display: flex;
      flex-direction: column;
      justify-content: center;
      text-align: center;
      border-left:0.02rem #c6c6c6 solid;
    }
  }
</style>
