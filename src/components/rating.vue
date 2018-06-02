<template>
  <div>
    <div class="rating" ref="ratings">
      <div class="rating-content">
        <div class="overflow">
          <div class="overflow-left">
            <h1 class="score">{{ seller.score }}</h1>
            <div class="title">综合评分</div>
            <div class="rank">高于周边商家的{{ seller.rankRate }}%</div>
          </div>
          <div class="overflow-right">
            <div class="score-wrapper">
              <span class="title">服务态度</span>
              <star :size="36" :score="seller.serviceScore"></star>
              <span class="score">{{ seller.serviceScore }}</span>
            </div>
            <div class="score-wrapper">
              <span class="title">商品评分</span>
              <star :size="36" :score="seller.foodScore"></star>
              <span class="score">{{ seller.foodScore }}</span>
            </div>
            <div class="delivery-wrapper">
              <span class="title">送达时间</span>
              <span class="delivery">{{ seller.deliveryTime }}分钟</span>
            </div>
          </div>
        </div>
        <split></split>
        <ratingselect @onlyContentChange='onlyContentChange' @typeChange='typeChange' :only-content='onlyContent' :select-type='selectType' :ratings='ratings'></ratingselect>
        <div class="rating-wrapper">
          <ul>
            <li class="rating-item" v-show="rateShow(items.rateType,items.text)" v-for="items in ratings">
              <div class="avatar">
                <img :src="items.avatar" width="28" height="28"/>
              </div> 
              <div class="content">
                <div class="name">{{ items.username }}</div>
                <div class="star-wrapper">
                  <star :size="24" :score="items.score"></star>
                  <span class="delivery" v-show="items.deliveryTime">{{ items.deliveryTime }}分钟送达</span>
                </div>
                <p class="text">{{ items.text }}</p>
                <div class="recommend" v-show="items.recommend && items.recommend.length">
                  <span class="icon-thumb_up"></span>
                  <span class="item" v-for="(item,index) in items.recommend">{{ items.recommend[index] }}</span>
                </div>
                <div class="time">{{items.rateTime|format}}</div>
              </div>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import iscroll from "../../node_modules/iscroll/build/iscroll-probe";
import star from "./star";
import ratingselect from "./ratingselect";
import { formatDate } from "../assets/js/formatDate";
import split from "./split";

const ERR_OK = 0;

//评论类型
const ALL = 2;
const POSITIVE = 0;
const NAGATIVE = 1;

export default {
  props: {
    seller: {
      type: Object
    }
  },
  data() {
    return {
      ratings: [],
      selectType: ALL,
      onlyContent: false
    };
  },
  created() {
    this.$http.get("/api/ratings").then(
      response => {
        if (response.data.errno === ERR_OK) {
          this.ratings = response.data.data;
          this.$nextTick(() => {
            this.scroll = new iscroll(this.$refs.ratings, {
              click: true
            });
          });
        }
      },
      response => {
        console.log("data wrong or no data");
      }
    );
  },
  methods: {
    rateShow(type, text) {
      if (this.foodList === false) {
        //当食品列表为空,隐藏评论列表
        return false;
      } else if (this.onlyContent && !text) {
        //如果勾选内容选项，没有内容评论,则隐藏评论列表
        return false;
      } else {
        if (this.selectType === ALL) {
          return true;
        } else {
          return this.selectType === type;
        }
      }
    },
    typeChange(type) {
      this.selectType = type;
      this.$nextTick(() => {
        this.scroll.refresh();
      });
    },
    onlyContentChange() {
      this.onlyContent = !this.onlyContent;
      this.$nextTick(() => {
        this.scroll.refresh();
      });
    }
  },
  filters: {
    format(time) {
      return formatDate(new Date(time), "yyyy-MM-dd hh:mm:ss");
    }
  },
  components: {
    star,
    ratingselect,
    split
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang='stylus'>
@import '../common/stylus/mixin.styl'

.rating 
  touch-action: none
  position: absolute
  top: 175px
  bottom: 48px
  width: 100%
  overflow: hidden
  .overflow 
    display: flex
    padding: 18px 0
    .overflow-left 
      padding: 6px 0
      flex: 0 0 137px
      width: 137px
      text-align: center
      border-right: 1px solid rgba(7, 17, 27, 0.1)
      .score 
        font-size: 24px
        margin-bottom: 6px
        color: #f90
        line-height: 28px
      .title 
        font-size: 12px
        margin-bottom: 8px
        color: #93999f
        line-height: 12px
      .rank 
        font-size: 10px
        color: #93999f
        line-height: 10px
    .overflow-right 
      font-size: 12px
      padding: 6px 0 6px 24px
      flex: 1
      .score-wrapper 
        margin-bottom: 8px
        font-size: 0
        .star 
          margin: 0 12px
        .score 
          color: #f90
        .title,.score
          display: inline-block
          line-height: 18px
          font-size: 12px
          vertical-align: top
      .delivery-wrapper 
        .delivery 
          font-size: 12px
          margin-left: 10px
          color: #93999f
  .rating-content 
    .split 
      width: 100%
      height: 16px
      border-top: 1px solid rgba(7, 17, 27, 0.1)
      border-bottom: 1px solid rgba(7, 17, 27, 0.1)
      background: #f3f5f7
  .rating-wrapper 
    padding: 0 18px
    .rating-item 
      padding: 18px 0
      display: flex
      position: relative
      .avatar 
        img 
          border-radius: 50%
      .content 
        margin-left: 10px
        font-size: 0
        .name 
          font-size: 10px
          color: #07111b
          line-height: 12px
          margin-bottom: 6px
        .star-wrapper 
          .delivery 
            display: inline-block
            font-size: 10px
            margin-left: 5px
            color: #93999f
            vertical-align: top
            margin-bottom: 8px
        .text 
          font-size: 12px
          margin-bottom: 8px
          line-height: 18px
        .recommend 
          font-size: 10px
          .icon-thumb_up{
            color #00a0dc
          }
          .item 
            font-size: 10px
            padding: 3px 5px
            margin-right: 8px
            color: #93999f
            border-1px(rgba(7, 17, 27, 0.1))
        .time 
          position: absolute
          top: 18px
          right: 0
          font-size: 10px
          color: #93999f
</style>
