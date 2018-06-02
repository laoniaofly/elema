<template>
  <div class="header">
    <div class="content-wrapper">
        <div class="avatar">
          <img width="64" height="64" :src="headerData.avatar">
        </div>
        <div class="content">
          <div class="title">
            <span class="brand"></span>
            <span class="name">{{ headerData.name }}</span>
          </div>
          <div class="description">{{ headerData.description }}/{{ headerData.deliveryTime }}分钟到达</div>
          <div class="support" v-if="headerData.supports">
            <span class="icon decrease"></span>
            <span class="text">{{ headerData.supports[0].description }}</span>
          </div>
        </div>
        <div class="support-count" @click='showDetail' v-if="headerData.supports">
          <span class="count">{{ headerData.supports.length }}个<span class="icon-keyboard_arrow_right"></span></span> 
        </div>
    </div>
    <div class="bulletin-wrapper" @click='showDetail'>
      <span class="bulletin-title"></span>
      <span class="bullentin-text">{{ headerData.bulletin }}<i class="icon-keyboard_arrow_right"></i></span>
    </div>
    <div class="background">
      <img :src='headerData.avatar' width="100%" height="100%"/>
    </div>
    <div class="detail" v-if='isDetailShow' @click='hideDetail'>
      <div class="detail-wrapper clearfix">
        <div class="detail-content">
          <h1 class="name">{{ headerData.name }}</h1>
        <div class="star-wrapper">
          <star :size="48" :score="headerData.score"></star>
        </div>
          <div class="title">
            <div class="line"></div>
            <div class="text">优惠信息</div>
            <div class="line"></div>
          </div>
          <ul class="supports">
            <li class="supports-item">
              <span class="icon decrease"></span> 
              <span class="text">在线支付满28减5</span>
            </li>
            <li class="supports-item">
              <span class="icon discount"></span> 
              <span class="text">VC无限橙果汁全场8折</span>
            </li>
            <li class="supports-item">
              <span class="icon special"></span> 
              <span class="text">单人精彩套餐</span>
            </li>
            <li class="supports-item">
              <span class="icon invoice"></span> 
              <span class="text">该商家支持发票,请下单写好发票抬头</span>
            </li>
            <li class="supports-item">
              <span class="icon guarantee"></span> 
              <span class="text">已加入“外卖保”计划,食品安全保障</span>
            </li>
          </ul>
        <div class="title">
          <div class="line"></div>
          <div class="text">商家广告</div>
          <div class="line"></div>
        </div>
        <div class="bulletin">
          <p class="content">{{ headerData.bulletin }}</p>
        </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import star from '../star'

export default {
  props:{
    headerData:{
      type: Object
    //   default:() => {}
    }
  },
  data(){
    return {
      isDetailShow:false
    }
  },
  methods:{
    showDetail(){
      this.isDetailShow = true
    },
    hideDetail(){
      this.isDetailShow = false
    }
  },
  components:{
    star
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang='stylus' scoped>
@import '../../common/stylus/mixin.styl'
  .header 
    position: relative
    overflow: hidden
    color: #fff
    background-color: rgba(7,17,27,0.5)
    .content-wrapper 
      position: relative
      padding: 24px 12px 18px 24px
      font-size: 0
      .avatar 
        display: inline-block
        vertical-align: top
        border-radius: 2px
      .content 
        display: inline-block
        margin-left: 16px
        .title 
          margin: 2px 0 8px 0
          .brand 
            display: inline-block
            width: 30px
            height: 18px
            vertical-align: top
            bg-image('../../common/image/header/brand')
            background-size: 30px 18px
            background-repeat: no-repeat
          .name 
            margin-left: 6px
            font-size: 16px
            font-weight: bold
            line-height: 18px
        .description 
          margin-bottom: 10px
          line-height: 12px
          font-size: 12px
          font-weight: normal
        .support 
          margin: 10px 0 2px 0
          font-size: 10px
          .icon 
            display: inline-block
            width: 12px
            height: 12px
            margin-right: 4px
            vertical-align: middle
            background-size: 12px 12px
            background-repeat: no-repeat
            &.decrease 
              bg-image('../../common/image/header/decrease_1')
          .text 
            line-height: 12px
      .support-count 
        position: absolute
        bottom: 14px
        right: 12px
        line-height: 12px
        background-color: rgba(0,0,0,0.2)
        padding: 0 8px
        height: 24px
        text-align: center
        border-radius: 14px
        .count 
          vertical-align: top
          font-size: 10px
          line-height: 24px
        .icon-keyboard_arrow_right 
          margin-left: 3px
          font-size: 10px
          line-height: 24px
    .bulletin-wrapper 
      position: relative
      height: 28px
      padding: 0 22px 0 12px
      white-space: nowrap
      overflow: hidden
      text-overflow: ellipsis
      background: rgba(7,17,27,0.1)
      .bulletin-title 
        display: inline-block
        width: 22px
        height: 12px
        bg-image('../../common/image/header/bulletin')
        background-size: 22px 12px
        background-repeat: no-repeat
        vertical-align: middle
      .bullentin-text 
        font-size: 10px
        line-height: 28px
        vertical-align: middle
        padding-left: 0
      .icon-keyboard_arrow_right
        position absolute
        right 10px
        top 10px
        font-size 10px
    .background 
      position: absolute
      top: 0
      left: 0
      width: 100%
      height: 100%
      z-index: -1
      filter: blur(10px)
    .detail 
      position: fixed
      top: 0
      left: 0
      width: 100%
      height: 100%
      background: rgba(7,17,27,0.8)
      overflow: auto
      z-index: 100
      transition: all 0.5s
      .detail-wrapper 
        min-height: 100%
        width: 100%
        .detail-content 
          margin-top: 64px
          padding-bottom: 64px
          .name 
            line-height: 16px
            font-size: 16px
            font-weight: 700
            text-align: center
          .star-wrapper 
            margin-top: 18px
            padding: 2px 0
            text-align: center
            margin-top: 18px
            text-align: center
            padding: 2px 0
          .title 
            display: flex
            width: 80%
            margin: 28px auto 24px auto
            .line 
              flex: 1
              position: relative
              top: -6px
              border-bottom: 1px solid rgba(255,255,255,0.2)
          .text 
            padding: 0 12px
            font-size: 14px
            font-weight: 700
          .supports 
            margin: 0 auto
            width: 80%
            .supports-item 
              font-size: 0
              margin-bottom: 10px
              padding: 0 12px
              .text 
                font-size: 12px
                line-height: 16px
                font-weight: normal
              .icon 
                display: inline-block
                width: 16px
                height: 16px
                background-size: 16px 16px
                margin-right: 10px
                vertical-align: top
                &.decrease 
                  bg-image('../../common/image/header/decrease_1')
                &.discount 
                  bg-image('../../common/image/header/discount_1')
                &.special 
                  bg-image('../../common/image/header/special_1')
                &.invoice 
                  bg-image('../../common/image/header/invoice_1')
                &.guarantee 
                  bg-image('../../common/image/header/guarantee_1')
          .bulletin 
            width: 80%
            margin: 0 auto
            .content 
              padding: 0 12px
              margin-bottom: 16px
              font-size: 12px
              line-height: 24px
</style>
