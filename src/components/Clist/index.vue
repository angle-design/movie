<template>
    <div class="cinema_body">
      <ul>
        <!--<li>-->
          <!--<div>-->
            <!--<span>大地影院</span>-->
            <!--<span class="q"><span class="price">22.9</span>元起</span>-->
          <!--</div>-->
          <!--<div class="address">-->
            <!--<span>区谁能思考A阿克苏拉开拉克</span>-->
            <!--<span>17229.6km</span>-->
          <!--</div>-->
          <!--<div class="card">-->
            <!--<div>小吃</div>-->
            <!--<div>折扣卡</div>-->
          <!--</div>-->
        <!--</li>-->
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
    </div>
</template>

<script>
    export default {
        name: "clist",
      data(){
          return{
            cinemaList:[]
          }
      },
      mounted(){
          this.axios.get('/api/cinemaList?cityId=10').then(res=>{
            var msg=res.data.msg;
            if(msg==='ok'){
              this.cinemaList=res.data.data.cinemas;
            }
          })
      },
      filters:{
          formatCard(key){
              var card=[
                {key:'allowRefund',value:'改签'},
                {key:'endorse',value:'退'},
                {key:'sell',value:'折扣卡'},
                {key:'snack',value:'小吃'},
              ];
              for(var i=0;i<card.length;i++){
                if(card[i].key===key){
                  return card[i].value;
                }
              }
              return '';
          },
        classCard(key){
          var card=[
            {key:'allowRefund',value:'bl'},
            {key:'endorse',value:'bl'},
            {key:'sell',value:'or'},
            {key:'snack',value:'or'},
          ];
          for(var i=0;i<card.length;i++){
            if(card[i].key===key){
              return card[i].value;
            }
          }
          return '';
        }
      }
    }
</script>

<style scoped lang="less">
    .cinema_body{
      flex:1;
      overflow:auto;
      ul{
        padding:0.4rem;
        li{
          border-bottom:0.02rem solid #E6E6E6;
          margin-bottom:0.4rem;
          div{
            margin-bottom:0.2rem;
            .q{
              font-size:0.22rem;color:#f03d37;
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
            &.card{
                display: flex;
                div{
                  padding:0 0.06rem;
                  height:0.3rem;
                  display: flex;
                  align-items: center;
                  border-radius:0.04rem;
                  color:#f90;
                  font-size:0.28rem;
                  border:0.02rem solid #f90;
                  margin-right:0.1rem;
                  &.or{
                    color:#f90;
                    border:0.02rem solid #f90;
                  }
                  &.bl{
                    color:#589daf;
                    border:0.02rem solid #589daf;
                  }
                }
              }
            }
          }

        }
      }
</style>
