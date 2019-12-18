<template>
  <div class="search_body">
    <div class="search_input">
      <div class="search_input_wrapper">
        <input type="text" v-model="message">
      </div>
    </div>
    <div class="search_result">
      <h3>电影/喜剧/综艺</h3>
      <ul>
        <li v-for="item in movieList" :key="item.id">
          <div class="img">
            <img :src="item.img | setWH('128.180')">
          </div>
          <div class="info">
            <p><span>{{item.nm}}</span><span>{{item.sc}}</span></p>
            <p>{{item.enm}}</p>
            <p>{{item.cat}}</p>
            <p>{{item.rt}}</p>
          </div>
        </li>

      </ul>
    </div>
  </div>
</template>

<script>
  export default {
    name: "search",
    data() {
      return {
        message: "",
        movieList: []
      }
    },
    methods: {
      cancelRequest() {
        if (typeof this.source === "function") {
          this.source('中止请求')
        }
      }
    },
    watch: {
      message(newval) {
        var that = this;
        var cityId = this.$store.state.city.id;
        this.cancelRequest()
        this.axios.get('/api/searchList?cityId=' + cityId + '&kw=' + newval, {
          cancelToken: new this.axios.CancelToken(function executor(c) {
            that.source = c
          })
        }).then((res) => {
          var msg = res.data.msg;
          var movies = res.data.data.movies;
          if (msg && movies) {
            this.movieList = res.data.data.movies.list;
          }
        }).catch((err) => {
          if (this.axios.isCancel(err)) {
            console.log('Rquest canceled', err.message); //请求如果被取消，这里是返回取消的message
          } else {
            //handle error
            console.log(err);
          }
        })
      }
    }
  }
</script>

<style scoped lang="less">
  .search_body {
    flex: 1;
    overflow: auto;
    .search_input {
      padding: 0.16rem 0.2rem;
      background: #f5f5f5;
      border-bottom: 0.02rem solid #e5e5e5;

      .search_input_wrapper {
        padding: 0 0.2rem;
        border: 0.02rem solid #e6e6e6;
        border-radius: 0.1rem;
        background: #fff;

        input {
          border: none;
          font-size: 0.26rem;
          color: #333;
          padding: 0.08rem 0;
          outline: none;
          margin-left: 0.2rem;
        }
      }
    }
    .search_result {
      h3 {
        font-size: 0.3rem;
        color: #999;
        padding: 0.18rem 0.3rem;
        border-bottom: 0.02rem solid #e6e6e6;
      }
      ul {
        li {
          border-bottom: 0.02rem solid #c9c9c9;
          padding: 0.18rem 0.3rem;
          box-sizing: border-box;
          display: flex;

          .img {
            width: 1.2rem;
            float: left;

            img {
              width: 100%;
            }
          }

          .info {
            float: left;
            margin-left: 0.3rem;
            flex: 1;

            p {
              height: 0.44rem;
              display: flex;
              line-height: 0.44rem;
              font-size: 0.24rem;

              &:nth-of-type(1) {
                span {
                  &:nth-of-type(1) {
                    font-size: 0.36rem;
                    flex: 1;
                  }

                  &:nth-of-type(2) {
                    font-size: 0.32rem;
                    color: #f7c103
                  }
                }
              }
            }
          }
        }
      }
    }
  }
</style>
