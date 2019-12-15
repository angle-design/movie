<template>
  <div class="search_body">
    <div class="search_input">
      <div class="search_input_wrapper">
        <input type="text">
      </div>
    </div>
    <div class="search_result">
      <h3>电影/喜剧/综艺</h3>
      <ul>
        <li>
          <div class="img">
            <img src="/static/images/qian.jpg" alt="">
          </div>
          <div class="info">
            <p><span>无名之辈</span><span>8.5</span></p>
            <p>A cool Ficsh</p>
            <p>剧情，喜剧，犯罪</p>
            <p>2018-11-16</p>
          </div>
        </li>
        <li>
          <div class="img">
            <img src="/static/images/qian.jpg" alt="">
          </div>
          <div class="info">
            <p><span>无名之辈</span><span>8.5</span></p>
            <p>A cool Ficsh</p>
            <p>剧情，喜剧，犯罪</p>
            <p>2018-11-16</p>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
  export default {
    name: "search"
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
