<template>
  <div class="seller" ref="seller">
    <div class="seller-content">
      <div class="overview">
        <h1 class="title">{{ seller.name }}</h1>
        <div class="desc">
          <star :size="36" :score="seller.score"></star>
          <span class="text">({{ seller.ratingCount }})</span>
          <span class="text">月销{{ seller.sellCount }}单</span>
        </div>
        <ul class="remark">
          <li class="block">
            <h2>{{ remark.qsPrice }}</h2>
            <div class="content"><span class="stress">{{ seller.minPrice }}</span>元</div>
          </li>
          <li class="block">
            <h2>{{ remark.jspsPrice }}</h2>
            <div class="content"><span class="stress">{{ seller.deliveryPrice }}</span>元</div>
          </li>
          <li class="block">
            <h2>{{ remark.psTime }}</h2>
            <div class="content"><span class="stress">{{ seller.deliveryTime }}</span>分钟</div>
          </li>
        </ul>
        <div class="favorite">
          <span class="icon-favorite" :class="{active:favActive}" @click.stop.prevent="toggleActive"></span>
          <span class="text">{{ favActive?'已收藏':'收藏' }}</span>
        </div>
      </div>
      <split></split>
      <div class="bulletin">
        <h1 class="title">{{ sellerMsg.sjgg }}</h1>
        <div class="content-wrapper">
          <p class="content">{{ seller.bulletin }}</p>
        </div>
        <ul class="supports">
          <li class="supports-item border-1px" v-for="(supprt,index) in seller.supports">
            <span class="icon" :class="classMap[seller.supports[index].type]"></span>
            <span class="text">{{ seller.supports[index].description }}</span>
          </li>
        </ul>
      </div>
      <split></split>
      <div class="pics">
        <h1 class="title">{{ sellerMsg.sjsj }}</h1>
        <div class="pic-wrapper" ref="picwrapper">
          <ul class="pic-list" ref="piclist">
            <li class="pic-item" v-for="(pic,index) in seller.pics">
              <img :src="seller.pics[index]" width="120" height="90" alt="" />
            </li>
          </ul>
        </div>
      </div>
      <split></split>
      <div class="info">
        <h1 class="title">{{ sellerMsg.sjxx }}</h1>
        <ul>
          <li class="info-item border-1px" v-for="(info,index) in seller.infos">{{ seller.infos[index] }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import split from './split'
import star from './star'
import iscroll from '../../node_modules/iscroll/build/iscroll-probe'

export default {
  props:{
    seller:{
      type:Object
    }
  },
  data () {
    return {
    favActive:false,
    sellerMsg:{sjgg:'商家公告',sjsj:'商家实景',sjxx:'商家信息'},
    remark:{qsPrice:'起送价',jspsPrice:'商家配送',psTime:'平均配送时间'},
    classMap:['decrease','discount','special','invoice','guarantee']
    }
  },
  methods:{
  _initScroll(){
    if(!this.sellerScroll){
      this.sellerScroll = new iscroll(this.$refs.seller,{
        click:true
      });
    }else{
      this.sellerScroll.refresh();
    }
  },
  _initLScroll(){
    if(this.seller.pics){
      let picWidth = 120,
        margin = 6,
        width = (picWidth+margin)*this.seller.pics.length - margin;
      this.$refs.piclist.style.width = width + "px";
      if(!this.picwrapper){
        this.picwrapper = new iscroll(this.$refs.picwrapper,{
          scrollX:true,
          eventPassthrough: 'vertical'
        });
      }else{
        this.picwrapper.refresh();
      }
    }
  },
  toggleActive(){
    this.favActive = !this.favActive;
    this.$nextTick(()=>{
      this.sellerScroll.refresh();
    });
  }
  },
  mounted(){
    this._initScroll();
    this._initLScroll();
  },
  watch:{
    seller(){
      this.$nextTick(() => {
        this._initScroll();
        this._initLScroll();
      })
    }
  },
  components:{
    split,
    star
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang='stylus'>
@import '../common/stylus/mixin.styl'

.seller 
  touch-action: none
  position: absolute
  top: 174px
  bottom: 48px
  overflow: hidden
  width: 100%
  .seller-content 
    .overview 
      position: relative
      padding: 18px
      .title 
        font-size: 14px
        margin-bottom: 8px
        line-height: 14px
        color: #07111b
      .desc 
        padding-bottom: 18px
        font-size: 0
        position: relative
        .star 
          margin-right: 8px
        .text 
          display: inline-block
          font-size: 10px
          color: #4d555d
          margin-right: 8px
          vertical-align: top
          line-height: 15px
      .remark 
        padding-top: 18px
        display: flex
        border-top: 1px solid rgba(7,17,27,0.1)
        .block 
          text-align: center
          border-right: 1px solid rgba(7,17,27,0.1)
          flex: 1
          &:last-child 
            border: none 
          h2 
            margin-bottom: 4px
            font-size: 10px
            color: #93999f
            line-height: 10px
          .content 
            font-size: 10px
            color: #07111b
          .stress 
            font-size: 24px
      .favorite 
        position: absolute
        top: 18px
        right: 11px
        width: 50px
        text-align: center
        .icon-favorite 
          display: block
          margin-bottom: 4px
          line-height: 24px
          font-size: 24px
          color: #d4d6d9
          &:before
            content "\E904"
          &.active 
            color: #f01414
        .text 
          margin: 0
          font-size 10px
    .bulletin 
      padding: 18px 18px 0 18px
      font-size: 0
      .title 
        font-size: 14px
        line-height: 14px
        margin-bottom: 8px
        color: #07111b
      .content-wrapper 
        padding: 0 12px 16px 12px
        display: flex
        .content 
          font-size: 12px
          color: #f01414
          line-height: 24px
      .supports 
        .supports-item
          padding: 16px 12px
          position: relative
          font-size: 0
          border-top: 1px solid rgba(7,17,27,0.1)
          .icon 
            display: inline-block
            width: 16px
            height: 16px
            background-size: 16px 16px
            margin-right: 6px
            background-repeat: no-repeat
            &.decrease 
              bg-image('../common/image/seller/decrease_4')
            &.discount 
              bg-image('../common/image/seller/discount_4')
            &.special 
              bg-image('../common/image/seller/special_4')
            &.invoice 
              bg-image('../common/image/seller/invoice_4')
            &.guarantee 
              bg-image('../common/image/seller/guarantee_4')
          .text 
            color: #07111b
            line-height: 16px
            font-size: 12px
            vertical-align: top
    .pics
      padding: 18px
      font-size: 0
      .title
        font-size: 14px 
        line-height: 14px
        margin-bottom: 8px
      .pic-wrapper 
        width: 100%
        overflow: hidden
        white-space: nowrap
      .pic-list 
        font-size: 0
        .pic-item 
          display: inline-block
          margin-right: 6px
          width: 120px
          height: 90px
    .info 
      padding: 18px 18px 0 18px
      .title
        font-size: 14px
        line-height: 14px
        margin-bottom: 8px
      .info-item 
        color: #07111b
        border-top: 1px solid rgba(7,17,27,0.1)
        padding: 16px 12px
        font-size: 12px
        line-height: 12px
</style>
