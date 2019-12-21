<template>
  <div class="movie_body">
    <Loading v-if="isLoading"></Loading>
    <scroller v-else>
      <ul>
        <li v-for="item in comingList" :key="item.id">
          <div class="pic_show"><img  @tap="handleToDetail(item.id)" :src="item.img | setWH('128.180')"/></div>
          <div class="info_list">
            <h2  @tap="handleToDetail(item.id)">{{item.nm}}<span v-if="item.version">3dmax</span></h2>
            <p><span class="person">{{item.wish}}</span>人想看</p>
            <p>主演：{{item.star}}</p>
            <p>{{item.rt}}}上映</p>
          </div>
          <div class="btn_mall">
            预售
          </div>
        </li>
      </ul>
    </scroller>
  </div>
</template>

<script>
  export default {
    name: "comming",
    data() {
      return {
        comingList: [],
        isLoading: true,
        prevCityId: -1
      }
    },
    activated() {
      var cityId = this.$store.state.city.id;
      if (this.prevCityId === cityId) {
        return;
      }
      this.isLoading = true;
      this.axios.get('/api/movieComingList?cityId=' + cityId).then((res) => {
        var msg = res.data.msg;
        if (msg === 'ok') {
          this.comingList = res.data.data.comingList;
          this.isLoading = false
          this.prevCityId = cityId
          console.log(res.data)
        }
      })
    },
    methods:{
      handleToDetail(movieid){
        this.$router.push('/movie/detail/2'+movieid)
      }
    }
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
            .person {
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
