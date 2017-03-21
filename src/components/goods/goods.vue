<template>
  <div class="goods">
    <div class="menu-wrapper" ref="menuWrapper">
      <ul>
        <li v-for="item in goods" class="menu-item">
          <span class="text">
            <i v-show="item.type>0" class="icon" :class="'icon-'+classMap[item.type]"></i>
            {{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper" ref="foodWrapper">
      <div>
        <dl v-for="item in goods" class="food-list">
            <dt class="title">{{item.name}}</dt>
            <dd v-for="food in item.foods" class="food-item">
                <div class="icon"><img :src="food.icon" /></div>
                <div class="content">
                   <h2 class="name">{{food.name}}</h2>
                   <p v-show="food.description" class="desc">{{food.description}}</p>
                   <div class="extra">
                      <span>月售{{food.sellCount}}份</span><span>好评率{{food.rating}}%</span>
                   </div>
                   <div class="price">
                      <span>￥{{food.price}}</span><span v-show="food.oldPrice">￥{{food.oldPrice}}</span>
                   </div>
                </div>
            </dd>
        </dl>
      </div>
    </div>
  </div>
</template>
<script>
import BScroll from "better-scroll";
export default {
  name: 'goods',
  props:{
    seller:{
      type:Object
    }
  },
  data(){
    return {
      goods:[]
    }
  },
  created(){
     this.classMap = ['decrease','discount','special','invoice','guarantee'];
     this.$http.get('/api/goods').then((response)=>{
      if(response.status===200){
          let rs = response.body
          if(rs.success){
              this.goods = rs.data;
              this.$nextTick(()=>{
                 this._initScroll();
              });
          }
      }
    })
  },
  methods:{
    _initScroll(){
      this.menuScroll = new BScroll(this.$refs.menuWrapper,{});
      this.foodsScroll = new BScroll(this.$refs.foodWrapper,{});
    }    
  }
}
</script>
<style lang="less" scoped>
@import "../../common/less/icon.less";
@import "../../common/less/main.less";
#app{
  .icon-decrease{
      background-image:url("../head/decrease_4@3x.png");
  }
  .icon-discount{
      background-image:url("../head/discount_4@3x.png");
  }
  .icon-guarantee{
      background-image:url("../head/guarantee_4@3x.png");
  }
  .icon-invoice{
      background-image:url("../head/invoice_4@3x.png");
  }
  .icon-special{
      background-image:url("../head/special_4@3x.png");
  }
  .goods{
    position:absolute;
    display:flex;
    overflow:hidden;
    width:100%;
    top:(48+128+36+56+80)/@r;
    bottom:92/@r;
    .menu-wrapper{
      flex: 0 0 160/@r;
      width:160/@r;
      background:#f3f5f7;
      .menu-item{
        display:table;
        height:108/@r;
        width:112/@r;
        padding:0 24/@r;
        line-height:28/@r;
        .icon{
          display:inline-block;
          float:left;
          width:24/@r;
          height:24/@r;
          background-size:24/@r 24/@r;
          background-repeat:no-repeat;
          background-position:center center;
        }
        .text{
          display:table-cell;
          width:112/@r;
          vertical-align:middle;
          font-size:24/@r;
          color:rgb(240,20,20);
          font-weight:200;
          .borderColor(0.2);
        }
      }
    }
    .foods-wrapper{
      flex:1;
      .title{
        padding-left:28/@r;
        border-left:4/@r solid #d9dde1;
        background:#f3f5f7;
        height:52/@r;
        line-height:52/@r;
        font-size:24/@r;
      }
      .food-item{
        display:flex;
        margin:36/@r;
        padding-bottom:36/@r;
        .borderColor(0.1);
        .icon{
          flex:0 0 114/@r;
          margin-right:20/@r;
        }
        .content{
          flex:1;
          .name{
            font-size:28/@r;
            color:rgb(7,17,27);
            height:28/@r;
            line-height:28/@r;
            margin:4/@r 0 16/@r;
          }
          .desc,.extra{
            color:rgb(147,153,159);
            line-height:20/@r;
            font-size:20/@r;
          }
          .desc{
            margin-bottom:16/@r;
            line-height:24/@r;
          }
          .extra{
            span:first-child{
              margin-right:24/@r;
            }
          }
          .price{
            font-weight:700;
            line-height:48/@r;
            :first-child{
              font-size:28/@r;
              color:rgb(240,20,20);
            }
            :last-child{
              text-decoration:line-through;
              font-size:20/@r;
              color:rgb(147,153,159);
            }
          }
        }
      }
      .food-item:last-child{
        border:none;
        margin-bottom:0;
      }
    }
  }
}

</style>
