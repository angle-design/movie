<template>
  <div class="cinema_body">
    <Loading v-if="isLoading"></Loading>
    <scroller v-else>
      <ul>
        <li v-for="item in cinemaList" :key="item.id">
          <div>
            <span>{{item.nm}}</span>
            <span class="q"><span class="price">{{item.sellPrice}}</span>元起</span>
          </div>
          <div class="address">
            <span>{{item.addr}}</span>
            <span>{{item.distance}}</span>
          </div>
          <div class="card">
            <div v-for="(num,key) in item.tag" v-if="num===1" :key="key" :class="key | classCard">
              {{key | formatCard}}
            </div>
          </div>
        </li>
      </ul>
    </scroller>
  </div>
</template>

<script>
  export default {
    name: "clist",
    data() {
      return {
        cinemaList: [],
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
      this.axios.get('/api/cinemaList?cityId=' + cityId).then(res => {
        var msg = res.data.msg;
        if (msg === 'ok') {
          this.cinemaList = res.data.data.cinemas;
          this.isLoading = false
          this.prevCityId = cityId
        }
      })
    },
    filters: {
      formatCard(key) {
        var card = [
          {key: 'allowRefund', value: '改签'},
          {key: 'endorse', value: '退'},
          {key: 'sell', value: '折扣卡'},
          {key: 'snack', value: '小吃'},
        ];
        for (var i = 0; i < card.length; i++) {
          if (card[i].key === key) {
            return card[i].value;
          }
        }
        return '';
      },
      classCard(key) {
        var card = [
          {key: 'allowRefund', value: 'bl'},
          {key: 'endorse', value: 'bl'},
          {key: 'sell', value: 'or'},
          {key: 'snack', value: 'or'},
        ];
        for (var i = 0; i < card.length; i++) {
          if (card[i].key === key) {
            return card[i].value;
          }
        }
        return '';
      }
    }
  }
</script>

<style scoped lang="less">
  .cinema_body {
    flex: 1;
    overflow: auto;
    ul {
      padding: 0.4rem;
      li {
        border-bottom: 0.02rem solid #E6E6E6;
        margin-bottom: 0.4rem;
        div {
          margin-bottom: 0.2rem;
          .q {
            font-size: 0.22rem;
            color: #f03d37;
            .price {
              font-size: 0.36rem;
            }
          }
          &.address {
            font-size: 0.26rem;
            color: #666;

            span {
              &:nth-of-type(2) {
                float: right;
              }
            }
          }
          &.card {
            display: flex;
            div {
              padding: 0 0.06rem;
              height: 0.3rem;
              display: flex;
              align-items: center;
              border-radius: 0.04rem;
              color: #f90;
              font-size: 0.28rem;
              border: 0.02rem solid #f90;
              margin-right: 0.1rem;
              &.or {
                color: #f90;
                border: 0.02rem solid #f90;
              }
              &.bl {
                color: #589daf;
                border: 0.02rem solid #589daf;
              }
            }
          }
        }
      }

    }
  }
</style>
