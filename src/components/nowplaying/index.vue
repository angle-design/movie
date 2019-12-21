<template>
  <div class="movie_body" ref="movie_body">
    <Loading v-if="isLoading"></Loading>
    <Scroller v-else :handleToScroll="handleToScroll" :handleToTouchEnd="handleToTouchEnd">
      <ul>
        <li class="pulldown">{{pullDownMsg}}</li>
        <li v-for="item in movieList" :key="item.id">
          <div class="pic_show"><img @tap="handleToDetail(item.id)" :src="item.img | setWH('128.180')"/></div>
          <div class="info_list">
            <h2  @tap="handleToDetail(item.id)">{{item.nm}}<span v-if="item.version">3dmax</span></h2>
            <p>观众评分<span class="grade">{{item.sc}}</span></p>
            <p>主演：{{item.star}}</p>
            <p>{{item.showInfo}}</p>
          </div>
          <div class="btn_mall">
            购票
          </div>
        </li>
      </ul>
    </Scroller>
  </div>
</template>

<script>
  // import Bscroll from 'better-scroll'
  export default {
    name: "nowplaying",
    data() {
      return {
        movieList: [],
        pullDownMsg: '',
        isLoading: true,
        prevCityId: -1
      }
    },
    methods: {
      handleToDetail(movieid) {
        this.$router.push('/movie/detail/1/'+movieid)
      },
      handleToScroll(pos) {
        if (pos.y > 30) {
          this.pullDownMsg = "正在更新中...."
        }
      },
      handleToTouchEnd(pos) {
        if (pos.y > 30) {
          this.axios.get('/api/movieOnInfoList?cityId=11').then(res => {
            var msg = res.data.msg;
            if (msg === 'ok') {
              this.pullDownMsg = "更新成功"
              setTimeout(() => {
                this.movieList = res.data.data.movieList;
                this.pullDownMsg = ""
              }, 1000)
            }
          })
        }
      }
    },
    activated() {
      var cityId = this.$store.state.city.id;
      if (this.prevCityId === cityId) {
        return;
      }
      this.isLoading = true;
      this.axios.get('/api/movieOnInfoList?cityId=' + cityId).then(res => {
        var msg = res.data.msg;
        if (msg === 'ok') {
          this.movieList = res.data.data.movieList;
          this.isLoading = false;
          this.prevCityId = cityId
          // this.$nextTick(()=>{
          //   var scroll=new Bscroll(this.$refs.movie_body,{
          //     tap:true,
          //     probeType:1
          //   })
          //   scroll.on('scroll',(pos)=>{
          //     // console.log('Scroller')
          //
          //     if(pos.y>30){
          //       this.pullDownMsg="正在更新中...."
          //     }
          //   })
          //   scroll.on('touchEnd',(pos)=>{
          //     // console.log('touchEnd')
          //     if(pos.y>30){
          //       this.axios.get('/api/movieOnInfoList?cityId=11').then(res=>{
          //         if(msg==='ok') {
          //           this.pullDownMsg="更新成功"
          //           setTimeout(()=>{
          //             this.movieList = res.data.data.movieList;
          //             this.pullDownMsg=""
          //           },1000)
          //
          //         }
          //       })
          //
          //     }
          //   })
          // });
        }
      })
    },

  }
</script>

<style scoped lang="less">
  .movie_body {
    flex: 1;
    overflow: auto;
    ul {
      margin: 0 0.24rem;
      overflow: hidden;
      li {
        display: flex;
        align-items: center;
        border-bottom: 0.02rem solid #eee;
        padding: 0.2rem 0.1rem;
        &.pulldown {
          padding: 0;
          margin: 0;
          border: none;
        }
        .pic_show {
          width: 1.28rem;
          height: 1.8rem;
          overflow: hidden;
          img {
            width: 100%;
          }
        }
        .info_list {
          margin-left: 0.1rem;
          flex: 1;
          position: relative;
          h2 {
            font-size: 0.34rem;
            line-height: 0.48rem;
            width: 3rem;
            overflow: hidden;
            white-space: nowrap;
            font-weight: bold;
            span {
              font-size: 0.26rem;
              color: #ff0000;
            }
          }
          p {
            font-size: 0.26rem;
            color: #666;
            line-height: 0.44rem;
            width: 4rem;
            overflow: hidden;
            white-space: nowrap;
            .grade {
              font-weight: 700;
              color: #faaf00;
              font-size: 0.3rem;
            }
          }
          img {
            width: 1rem;
            position: absolute;
            right: 0.2rem;
            top: 0.1rem;
          }
        }
        .btn_mall, .btn_pre {
          width: 0.94rem;
          height: 0.54rem;
          line-height: 0.54rem;
          text-align: center;
          background: #ef4238;
          color: #fff;
          border-radius: 0.15rem;
        }
      }
    }
  }
</style>
