<template>
  <div class="goods">
    <div class="menu-wrapper">
      <ul>
        <li v-for="item in goods" class="menu-item">
          <span class="text border-1px">
            <span v-show="item.type>0" class="icon" :class=""></span>
            {{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper">

    </div>
  </div>
</template>
<script>
  const ERR_OK = 0;
  export default {
    prop: {
      seller: {
        type: Object
      }
    },
    data() {
      return {
        goods: []
      };
    },
    created() {
      this.$http.get('/api/goods').then((response) => {
        response = response.body;
        console.log(response);
        if (response.errno === ERR_OK) {
          this.goods = response.data;
        };
      }, response => {
        // error callback
      });
    }
  };
</script>
<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl"
  .goods
    display:flex
    position:absolute
    width:100%
    top:174px
    bottom:46px
    overflow:hidden
    .menu-wrapper
      flex:0 0 80px
      // 兼容问题
      width:80px
      background:#f3f5f7
      .menu-item
        display:table
        padding:0 12px
        height:54px
        width:56px;
        line-height:14px
        .text
          display:table-cell
          width:56px
          vertical-align:middle
          border-1px(rgba(7,17,27,0.1))
          font-size:12px
    .foods-wrapper
      flex:1
</style>