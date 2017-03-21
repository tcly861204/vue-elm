<template>
<div class="star" :class="starType">
   <span v-for="itemClass in itemClasses" :class="itemClass" class="star-item"></span>
</div>
</template>
<script>
const LENGTH = 5;
const CLS_ON = 'on';
const CLS_HALF = 'half';
const CLS_OFF = 'off';
export default {
  props:{
    size:{
        type:Number
    },
    score:{
        type:Number
    }
  },
  computed:{
    starType(){
        return "star-"+this.size;
    },
    itemClasses(){
        let result = [];
        let score = this.score;
        if(score){
          for(var i=1;i<=score;i++){
            result.push(CLS_ON);
          }
          let scoreStr = score+'';
          if(scoreStr.indexOf('.')>0){
             if(scoreStr.split('.')[1]>=5){
                 result.push(CLS_HALF);
             }else{
                 result.push(CLS_OFF);
             }
          } 
          while(result.length<5){
              result.push(CLS_OFF);
          }
        }
        return result;
    }
  }
}
</script>
<style lang="less" scoped>
@import "../../common/less/main.less";
.star{
    font-size:0;
    text-align:center;
    .star-item{
        display:inline-block;
    }
}
.star-48{
    height:57/@r;
    .star-item{
        width:60/@r;
        height:57/@r;
        background-repeat:no-repeat;
        background-size:60/@r 57/@r;
        margin-right:44/@r;
    }
    .on{
        background-image:url('star48_on@3x.png');
    }
    .half{
        background-image:url('star48_half@3x.png');
    }
    .off{
        background-image:url('star48_off@3x.png');
    }
    :last-child{
        margin-right:0;
    }
}
.star-36{
    height:44/@r;
    .star-item{
        width:45/@r;
        height:44/@r;
        background-repeat:no-repeat;
        background-size:45/@r 44/@r;
        margin-right:34/@r;
    }
    .on{
        background-image:url('star36_on@3x.png');
    }
    .half{
        background-image:url('star36_half@3x.png');
    }
    .off{
        background-image:url('star36_off@3x.png');
    }
    :last-child{
        margin-right:0;
    }
}
.star-24{
    height:29/@r;
    .star-item{
        width:30/@r;
        height:29/@r;
        background-repeat:no-repeat;
        background-size:30/@r 29/@r;
        margin-right:26/@r;
    }
    .on{
        background-image:url('star24_on@3x.png');
    }
    .half{
        background-image:url('star24_half@3x.png');
    }
    .off{
        background-image:url('star24_off@3x.png');
    }
    :last-child{
        margin-right:0;
    }
}



</style>