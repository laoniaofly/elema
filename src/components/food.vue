<template>
  <transition name="move">
    <div class="food" ref="food" v-show="foodShow">
      <div class="food-content">
        <div class="image_wrapper">
          <img :src="food.image" alt="" class="img">
          <div class="back" @click.stop.prevent="back">
            <i class="icon-arrow_lift"></i>
          </div>
        </div>
        <div class="content">
          <h1 class="title">{{ food.name }}</h1>
          <div class="detail">
            <span class="sell-count">月售{{ food.sellCount }}份</span>
            <span class="rating">好评率{{ food.rating }}%</span>
          </div>
          <div class="price">
            ￥<span class="now"> {{ food.price }}</span>
            <span class="old" v-show="food.oldPrice">￥{{ food.oldPrice }}</span>
          </div>
          <div class="buy" @click.stop.prevent="addCart" v-show="!food.count || food.count === 0">加入购物车</div>
          <div class="cartcontrol-wrapper" v-show="food.count && food.count>0">    
            <cartcontrol :food="food"></cartcontrol>
          </div>
        </div>
        <split v-show="food.info"></split>
        <div class="info" v-show="food.info">
          <h1 class="title">{{ foodMsg.spMsg }}</h1>
          <p class="text">{{ food.info }}</p>
        </div>
        <split></split>
        <div class="rating">
          <h1 class="title">{{ foodMsg.sppj }}</h1>
          <ratingSelect @onlyContentChange='onlyContentChange' @typeChange='typeChange' :only-content="onlyContent" :desc="desc" :select-type='selectType' :ratings='food.ratings'></ratingSelect>
          <div class="rating-wrapper">
            <ul v-show="food.ratings && food.ratings.length>0">
              <li class="rating-item border-1px" v-for="rating in food.ratings" v-show="needShow(rating.rateType,rating.text)">
                <div class="user">
                  <span class="name">{{ rating.username }}</span>
                  <img :src="rating.avatar" width="12" height="12">
                </div>
                <div class="time">{{ rating.rateTime | format }}</div>
                <p class="text">
                  <span class="icon-thump_up"></span>{{ rating.text }}
                </p>
              </li>
            </ul>
            <div v-show="!food.ratings || food.ratings.length===0" class="no-rating">暂无评价</div>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
import split from './split'
import iscroll from '../../node_modules/iscroll/build/iscroll-probe'
import ratingSelect from './ratingselect'
import { formatDate } from '../assets/js/formatDate' 
import cartcontrol from './cartcontrol'

const ALL=2;
const POSITIVE=0;
const NAGATIVE=1;

export default {
  props:{
    food:{
      type:Object
    },
    foodMsg:{
      type:Object,
      default:() => {
        return {
          spMsg:'商品信息',
          sppj:'商品评价'
        }
      }
    },
  desc:{
    type: Object,
    default: () => {
      return {
        all: '全部',
        positive: '推荐',
        nagative: '吐槽'
      };
    }
  }
  },
  data () {
    return {
    favActive:false,
    onlyContent:false,
    selectType: ALL,
    foodShow:false
    }
  },
  methods:{
    show(){
      this.foodShow=true;
      this.selectType=ALL;
      this.$nextTick(() => {
        if(!this.scroll){
          this.scroll = new iscroll(this.$refs.food,{
            click: true
          });
        }
      });
    },
    onlyContentChange(){
      this.onlyContent=!this.onlyContent;
      this.$nextTick(() => {
        this.scroll.refresh();
      });
    },
    typeChange(type){
      this.selectType = type;
      this.$nextTick(() => {
        this.scroll.refresh();
      });
    },
    back(){
      this.foodShow = false;
    },
    needShow(type,text){
      if(this.onlyContent && !text){
        return false;
      }else{
        if(this.selectType === ALL){
          return true;
        }else{
          return this.selectType === type;
        }
      }
    },
    addCart(){
      if(!this.food.count){
        this.$set(this.food,'count',1);
      }else{
        this.food.count++;
      }
    }
  },
  filters:{
    format(time){
      return formatDate(new Date(time),'yyyy-MM-dd hh:mm:ss');
    }
  },
  components:{
    split,
    ratingSelect,
    cartcontrol
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang='stylus'>

.food 
  touch-action: none
  position: fixed
  top: 0
  left: 0
  bottom: 48px
  z-index: 30
  width: 100%
  background: #fff
  transition: all 0.5s
  .food-content 
    .image_wrapper 
      position: relative
      width: 100%
      height: 0
      padding-top: 100%
      .img 
        position: absolute
        top: 0
        left: 0
        width: 100%
        height: 100%
      .back 
        position: absolute
        top: 0
        left: 0
        color: #fff
        padding: 8px
        border-radius: 50%
        margin: 10px 0 0 10px
    .content 
      position: relative
      padding: 19px
      .title 
        font-size: 14px
        margin-bottom: 8px
        font-weight: 700
        color: #07111b
        line-height: 14px
      .detail 
        font-size: 10px
        color: #93999f
        line-height: 10px
        font-size: 0
        margin-bottom: 18px
        .sell-count 
          font-size: 10px
          margin-right: 10px
        .rating 
          font-size: 10px
      .price 
        line-height: 24px
        font-size: 10px
        color: #f01414
        font-weight: 700
        .now 
          font-size: 14px
          margin-right: 6px
        .old 
          text-decoration: line-through
          color: #93999f
          font-size: 12px
      .buy
        position: absolute
        display: inline-block
        right: 18px
        bottom: 20px
        font-size: 10px
        background: #00a0dc
        color: #fff
        font-weight: 400
        line-height: 24px
        border-radius: 10px
        padding: 0 10px
      .cartcontrol-wrapper
        position: absolute
        right: 18px
        bottom: 20px
    .info 
      padding: 18px
      font-size: 0
      .title 
        font-size: 14px
        color: #07111b
        margin-bottom: 6px
        line-height: 14px
      .text 
        font-size: 12px
        color: #4d555d
        line-height: 24px
        padding: 0 2px
    .rating 
      padding-top: 18px
      .title 
        font-size: 14px
        line-height: 14px
        color: #07111b
        margin-left: 18px
      .rating-wrapper 
        padding: 0 18px
      .rating-item 
        position: relative
        padding: 18px 0
        .user 
          position: absolute
          display: inline-block
          top: 18px
          right: 18px
          font-size: 0
          .name 
            font-size: 10px
            color: #939d9f
            margin-right: 6px
            line-height: 12px
            vertical-align: top
          img 
            display: inline-block
            border-radius: 50%
        .time 
          font-size: 10px
          color: #939d9f
          line-height: 12px
          margin-bottom: 6px
        .text 
          font-size: 12px
          color: #07111b
          line-height: 17px
  &.move-enter,&.move-leave-active 
    transform: translate3d(100%,0,0)


</style> 

