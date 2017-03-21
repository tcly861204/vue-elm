<template>
  <div id="app">
    <v-head v-bind:seller="seller"></v-head>
    <div class="tab">
       <router-link to="/goods">商品</router-link>
       <router-link to="/ratings">评论</router-link>
       <router-link to="/seller">商家</router-link>
    </div>
    <router-view></router-view>
  </div>
</template>
<script>
import head from './components/head/head.vue'
export default {
  name: 'app',
  data(){
    return {
      seller:{}
    }
  },
  created(){
    this.$http.get('/api/seller').then((response)=>{
      if(response.status===200){
          let rs = response.body
          if(rs.success){
              this.seller = rs.data;
          }
      }
    })
  },
  components: { 'v-head':head}
}
</script>

<style lang="less" scoped>
@import "./common/less/icon.less";
@import "./common/less/main.less";
#app{
  height:100%;
  .tab{
     display:flex;
     width:100%;
     height:80/@r;
     line-height:80/@r;
     .borderColor(@apl:0.1);
     a{
        flex:1;
        display:block;
        text-align:center;
        font-size:28/@r;
        
     }
     a.router-link-active{
        color:rgba(240,20,20,1);
     }
  }
}
</style>
