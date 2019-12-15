<template>
  <div class="movie_body">
    <ul>
      <li>
        <div class="pic_show"><img src="/static/images/qian.jpg"/></div>
        <div class="info_list">
          <h2>无名之辈</h2>
          <p><span class="person">1766</span>人想看</p>
          <p>主演：陈建斌</p>
          <p>2018-11-30上映</p>
        </div>
        <div class="btn_mall">
          预售
        </div>
      </li>
      <li>
        <div class="pic_show"><img src="/static/images/qian.jpg"/></div>
        <div class="info_list">
          <h2>无名之辈</h2>
          <p><span class="person">1766</span>人想看</p>
          <p>主演：陈建斌</p>
          <p>2018-11-30上映</p>
        </div>
        <div class="btn_mall">
          预售
        </div>
      </li>  <li>
      <div class="pic_show"><img src="/static/images/qian.jpg"/></div>
      <div class="info_list">
        <h2>无名之辈</h2>
        <p><span class="person">1766</span>人想看</p>
        <p>主演：陈建斌</p>
        <p>2018-11-30上映</p>
      </div>
      <div class="btn_mall">
        预售
      </div>
    </li>
      <li>
        <div class="pic_show"><img src="/static/images/qian.jpg"/></div>
        <div class="info_list">
          <h2>无名之辈</h2>
          <p><span class="person">1766</span>人想看</p>
          <p>主演：陈建斌</p>
          <p>2018-11-30上映</p>
        </div>
        <div class="btn_mall">
          预售
        </div>
      </li>
      <li>
        <div class="pic_show"><img src="/static/images/qian.jpg"/></div>
        <div class="info_list">
          <h2>无名之辈</h2>
          <p><span class="person">1766</span>人想看</p>
          <p>主演：陈建斌</p>
          <p>2018-11-30上映</p>
        </div>
        <div class="btn_mall">
          预售
        </div>
      </li>

    </ul>
  </div>
</template>

<script>
    export default {
        name: "comming"
    }
</script>

<style scoped lang="less">
  .movie_body{
    flex:1;
    overflow: auto;
    ul{
      margin:0 0.24rem;
      overflow:hidden;
      li{
        display: flex;
        align-items: center;
        border-bottom:0.02rem solid #eee;
        padding:0.2rem 0.1rem;
        .pic_show{
          width:1.28rem;
          height:1.8rem;
          overflow: hidden;
          img{
            width:100%;
          }
        }
        .info_list{
          margin-left:0.1rem;
          flex: 1;
          position: relative;
          h2{
            font-size:0.34rem;
            line-height:0.48rem;
            width:3rem;
            overflow: hidden;
            white-space: nowrap;
            font-weight: bold;
          }
          p{
            font-size:0.26rem;
            color:#666;
            line-height:0.44rem;
            width:4rem;
            overflow: hidden;
            white-space: nowrap;
            .person{
              font-weight:700;
              color:#faaf00;
              font-size:0.3rem;
            }
          }
          img{
            width:1rem;
            position: absolute;
            right:0.2rem;
            top:0.1rem;
          }
        }
        .btn_mall,.btn_pre{
          width:0.94rem;
          height:0.54rem;
          line-height:0.54rem;
          text-align: center;
          background: #ef4238;
          color:#fff;
          border-radius:0.15rem;
        }
      }
    }
  }
</style>
