<template>
  <div class="header">
    <div class="content-wrapper clearfix">
       <div class="avatar">
          <img :src="seller.avatar" />
       </div>
       <div class="content">
          <div class="title clearfix">
             <div class="brand"></div>
             <div class="name">{{seller.name}}</div>
          </div>
          <div class="description">
             {{seller.description}}/{{seller.deliveryTime}}分钟送达
          </div>
          <div v-if="seller.supports" class="support clearfix">
             <span class="icon" :class="'icon-'+classMap[seller.supports[0].type]"></span>
             <span class="text">{{seller.supports[0].description}}</span>
          </div>
       </div>
       <div v-if="seller.supports" class="support-count clearfix" @click="showDetail">
           <span class="count">{{seller.supports.length}}个</span>
           <span class="font-icon icon-keyboard_arrow_right"></span>
       </div>
    </div>
    <div class="bulletin-wrapper clearfix" @click="showDetail">
      <div class="bulletin-title"></div>
      <div class="bulletin-text">{{seller.bulletin}}</div>
      <span class="font-icon icon-keyboard_arrow_right"></span>
    </div>
    <div class="background">
      <img :src="seller.avatar"/>
    </div>
    <div v-show="detailShow" class="detail">
      <div class="detail-wrapper clearfix">
         <div class="detail-main">
            <h1 class="detail-name">{{seller.name}}</h1>
            <v-star :score="seller.score" :size="48"></v-star>
            <div class="detail-title">
               <div class="line"></div>
               <div class="text">优惠信息</div>
               <div class="line"></div>
            </div>
            <ul v-if="seller.supports" class="detail-content">
               <li class="support-item" v-for="supportItem in seller.supports">
                  <i class="icon" :class="'icon-'+classMap[supportItem.type]"></i>{{supportItem.description}}
               </li>
            </ul>
            <div class="detail-title">
               <div class="line"></div>
               <div class="text">商家公告</div>
               <div class="line"></div>
            </div>
            <div class="detail-content">
                <p class="detail-bulletin">{{seller.bulletin}}</p>
            </div>
         </div>
      </div>
      <div class="detail-close" @click="detailClose">
         <span class="icon-close"></span>
      </div>
    </div>
  </div>
</template>
<script>
import Star from "../star/star"
export default {
  props:{
    seller:{
      type:Object
    }
  },
  data(){
    return {
      detailShow:false
    }
  },
  created(){
    this.classMap = ['decrease','discount','special','invoice','guarantee'];
  },
  methods:{
    showDetail(){
      this.detailShow = true;
    },
    detailClose(){
      this.detailShow = false;
    }
  },
  components:{
    'v-star':Star
  }
}
</script>
<style lang="less" scoped>
@import "../../common/less/icon.less";
@import "../../common/less/main.less";
#app{
  .icon-decrease{
      background-image:url("decrease_2@3x.png");
  }
  .icon-discount{
      background-image:url("discount_2@3x.png");
  }
  .icon-guarantee{
      background-image:url("guarantee_2@3x.png");
  }
  .icon-invoice{
      background-image:url("invoice_2@3x.png");
  }
  .icon-special{
      background-image:url("special_2@3x.png");
  }
  .header{
     color:#fff;
     position:relative;
     .bgColor(0.3);
     overflow:hidden;
     .content-wrapper{
        padding:48/@r 24/@r 36/@r 48/@r;
        position:relative;
        .avatar{
          width:128/@r;
          height:128/@r;
          float:left;
          img{
            display:block;
            width:128/@r;
            height:128/@r;
            border-radius:4/@r;
          }
        }
        .content{
          float:left;
          margin:0 0 0 32/@r;
          height:128/@r;
          .title{
            margin: 4/@r 0 8/@r 0;
            height:36/@r;
            .brand{
              float:left;
              width:60/@r;
              height:36/@r;
              background:url("brand@3x.png") no-repeat center center;
              background-size:60/@r 36/@r;
            }
            .name{
              float:left;
              margin: 0 0 0 12/@r;
              height:36/@r;
              line-height:36/@r;
              font-size:32/@r;
              font-weight:bold;
            }
          }
          .description{
            font-size:24/@r;
            line-height:24/@r;
            font-weight:200;
            margin-bottom:20/@r;
          }
          .support{
            height:24/@r;
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
              display:inline-block;
              float:left;
              line-height:24/@r;
              font-size:20/@r;
              margin-left:8/@r;
            }
          }
        }
        .support-count{
            position:absolute;
            right:24/@r;
            bottom:36/@r;
            height:24/@r;
            line-height:24/@r;
            padding:14/@r 16/@r;
            border-radius:48/@r;
            background:rgba(0,0,0,0.2);
            font-size:20/@r;
            width:62/@r;
            color:#fff;
            .count,.font-icon{
              display:inline-block;
              padding:0;
              margin:0;
              height:24/@r;
              text-align:center;
            }
            .count{
              width:36/@r;
            }
            .font-icon{
              width:16/@r;
              margin-left:4/@r;
            }
        }
     }
     .bulletin-wrapper{
       height:56/@r;
       .bgColor(0.2);
       line-height:56/@r;
       width:15rem;
       font-size:0;
       .bulletin-title{
         padding:10/@r 8/@r 10/@r 24/@r;
         width:66/@r;
         height:36/@r;
         background:url('bulletin@3x.png') no-repeat 24/@r center;
         background-size:66/@r 36/@r;
         float:left;
       }
       .bulletin-text{
         font-size:20/@r;
         white-space:nowrap;
         text-space:1;
         overflow:hidden;
         text-overflow:ellipsis;
         float:left;
         width:(750-56-32-66)/@r;
       }
       .font-icon{
          width:56/@r;
          height:56/@r;
          line-height:56/@r;
          display:block;
          text-align:center;
          float:right;
          font-size:20/@r;
       }
     }
     .background{
       position:absolute;
       top:0;
       left:0;
       width:100%;
       height:(48+36+128+56)/@r;
       z-index:-1;
       img{
         width:100%;
         height:100%;
         display:block;
         filter:blur(15/@r);
       }
     }
     .detail{
       position:fixed;
       z-index:100;
       width:100%;
       height:100%;
       overflow:auto;
       top:0;
       left:0;
       .bgColor(0.7);
       .detail-wrapper{
         min-height:100%;
         width:100%;
         .detail-main{
           padding:128/@r 0;
           .detail-name{
             font-size:32/@r;
             font-weight:700;
             line-height:32/@r;
             text-align:center;
             margin-bottom:32/@r;
           }
           .detail-title{
             margin:56/@r auto 48/@r;
             display:flex;
             padding:0 72/@r;
             .line{
               flex:1;
               position:relative;
               height:1/@r;
               background:rgba(255,255,255,0.2);
               top:14/@r;
             }
             .text{
               text-align:center;
               font-size:28/@r;
               line-height:28/@r;
               font-weight:700;
               color:#fff;
               padding:0 24/@r;
             }
           }
           .detail-content{
             padding:0 96/@r;
             .support-item{
               height:32/@r;
               margin: 0 0 24/@r 0;
               font-size:24/@r;
               font-weight:200;
               line-height:32/@r;
               .icon{
                 display:inline-block;
                 background-repeat:no-repeat;
                 width:32/@r;
                 height:32/@r;
                 background-size:32/@r 32/@r;
                 float:left;
                 padding-right:12/@r;
               }

             }
             .detail-bulletin{
               font-size:24/@r;
               font-weight:200;
               color:#fff;
               line-height:48/@r;
             }
           }
         }
       }
       .detail-close{
         position:relative;
         width:64/@r;
         height:64/@r;
         margin:-128/@r auto 0;
         font-size:64/@r;
       }
     }


  }
}
</style>
