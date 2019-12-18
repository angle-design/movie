<template>

  <div class="city_body">
    <Loading v-if="isLoading"></Loading>
    <div class="city_list" v-else>
      <Scroller ref="city_list">
        <div>
          <div class="city_hot">
            <h2>热门城市</h2>
            <ul class="clearfix">
              <li v-for="item in hotList" :key="item.id" @tap="handleToCity(item.nm,item.id)">{{item.nm}}</li>
            </ul>
          </div>
          <div class="city_sort" ref="city_sort">
            <div v-for="item in cityList" :key="item.index">
              <h2>{{item.index}}</h2>
              <ul>
                <li v-for="itemList in item.list" @tap="handleToCity(itemList.nm,itemList.id)" :key="itemList.id">
                  {{itemList.nm}}
                </li>
              </ul>
            </div>
          </div>
        </div>
      </Scroller>
    </div>
    <div class="city_index">
      <ul>
        <li v-for="(item,index) in cityList" :key="item.index" @touchstart="handleToIndex(index)">{{item.index}}</li>
      </ul>
    </div>
  </div>

</template>

<script>
  export default {
    name: "city",
    data() {
      return {
        cityList: [],
        hotList: [],
        isLoading: true
      }
    },
    mounted() {
      var cityList = window.localStorage.getItem('cityList');
      var hotList = window.localStorage.getItem('hotList')
      if (cityList && hotList) {
        this.isLoading = false
        this.cityList = JSON.parse(cityList);
        this.hotList = JSON.parse(hotList);
      } else {
        this.axios.get('/api/cityList').then(res => {
          var msg = res.data.msg;
          if (msg == 'ok') {
            this.isLoading = false
            var cities = res.data.data.cities;
            //[{index:'A',list:[{nm:'阿城',id:123}]}]
            var {cityList, hotList} = this.formatCityList(cities);
            this.cityList = cityList;
            this.hotList = hotList;
            window.localStorage.setItem('cityList', JSON.stringify(cityList))
            window.localStorage.setItem('hotList', JSON.stringify(hotList))
          }
        })
      }
    },
    methods: {
      formatCityList(cities) {
        var cityList = [];
        var hotList = [];
        for (var i = 0; i < cities.length; i++) {
          if (cities[i].isHot === 1) {
            hotList.push(cities[i])
          }
        }
        for (var i = 0; i < cities.length; i++) {
          var firstLetter = cities[i].py.substring(0, 1).toUpperCase();
          if (toCom(firstLetter)) {//新添加index
            cityList.push({index: firstLetter, list: [{nm: cities[i].nm, id: cities[i].id}]})
          } else {//累加到已有index
            for (var j = 0; j < cityList.length; j++) {
              if (cityList[j].index == firstLetter) {
                cityList[j].list.push({nm: cities[i].nm, id: cities[i].id})
              }
            }
          }
        }
        cityList.sort((n1, n2) => {
          if (n1.index > n2.index) {
            return 1;
          } else if (n1.index < n2.index) {
            return -1
          } else {
            return 0;
          }
        })

        function toCom(firstLetter) {
          for (var i = 0; i < cityList.length; i++) {
            if (cityList[i].index == firstLetter) {
              return false;
            }
          }
          return true;
        }

        return {
          cityList,
          hotList
        }
      },
      handleToIndex(index) {
        var h2 = this.$refs.city_sort.getElementsByTagName('h2');
        // this.$refs.city_sort.parentNode.scrollTop=h2[index].offsetTop;
        this.$refs.city_list.toScrollTop(-h2[index].offsetTop)
      },
      handleToCity(nm, id) {
        this.$store.commit("city/CITY_INFO", {nm, id});
        window.localStorage.setItem("nowNm", nm);
        window.localStorage.setItem("nowId", id);
        this.$router.push('/movie/nowplaying')
      }
    }
  }
</script>

<style scoped lang="less">
  .city_body {
    margin-top: 0.9rem;
    display: flex;
    width: 100%;
    position: absolute;
    top: 0;
    bottom: 0;

    .city_list {
      flex: 1;
      overflow: auto;
      background: #fff5f0;

      &::-webkit-scrollbar {
        background-color: transparent;
        width: 0;
      }

      .city_hot {
        margin-top: 0.4rem;

        h2 {
          padding-left: 0.3rem;
          line-height: 0.6rem;
          font-size: 0.28rem;
          background: #f0f0f0;
          font-weight: normal;
        }

        ul {
          overflow: auto;

          li {
            float: left;
            background: #fff;
            width: 29%;
            height: 0.66rem;
            margin-top: 0.3rem;
            margin-left: 3%;
            padding: 0.08rem;
            border: 0.02rem solid #c6c6c6;
            box-sizing: border-box;
            text-align: center;
          }
        }
      }

      .city_sort {
        div {
          margin-top: 0.4rem;

          h2 {
            padding-left: 0.3rem;
            line-height: 0.6rem;
            font-size: 0.28rem;
            background: #f0f0f0;
            font-weight: normal;
          }

          ul {
            padding-left: 0.2rem;
            margin-top: 0.2rem;

            li {
              line-height: 0.6rem;
            }
          }
        }
      }
    }

    .city_index {
      width: 0.4rem;
      display: flex;
      flex-direction: column;
      justify-content: center;
      text-align: center;
      border-left: 0.02rem #c6c6c6 solid;
    }
  }
</style>
