<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
      <div class="tab-item">
        <router-link class="link" to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link class="link" to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link class="link" to="/seller">商家</router-link>
      </div>
    </div>
    <keep-alive>
      <router-view :seller="seller"></router-view>
    </keep-alive>
  </div>
</template>

<script>
import header from './components/header/header';
var ERR_OK = 0;
export default{
  data() {
    return {
      seller: {}
    }
  },
  created() {
    this.$axios.get('/api/seller').then((result) => {
      result = result.data;
      if(result.errno === ERR_OK) {
        this.seller = result.data;
      }
    })
  },
  components:{
    'v-header':header,
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
@import "./common/stylus/mixin.styl";
.tab
  display: flex
  width: 100%
  height: 40px
  line-height: 40px
  border-1px(rgba(7, 17, 27, 0.1))
  .tab-item 
    flex: 1
    text-align: center
.link
  display: block
  font-size: 14px
  color: rgb(77, 85, 93)
a.router-link-active
  color: rgb(240, 20, 20)
</style>
