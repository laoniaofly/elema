<template>
  <div>
    <div class="shopcart">
      <div class="content">
        <div class="content-left">
          <div class="logo-wrapper">
            <div class="logo" :class="{active:totalCount>0}"><i class="icon-shopping_cart" :class="{active:totalCount>0}"></i></div>
            <div class="num" v-show="totalCount>0">{{ totalCount }}</div>
          </div>
          <div class="price" :class="{active:calcuPrice>0}">￥{{ calcuPrice }}元</div>
          <div class="description">另需配送费￥{{ seller.deliveryPrice }}元</div>
        </div>
        <div class="content-right">
          <div class="pay" :class="{active:calcuPrice>=seller.minPrice}" @click.stop.prevent="toPay">{{ caculate }}</div>
        </div>
      </div>
      <div class="ball-container">
        <div>
          <div class="ball">
            <div class="inner inner-hook"></div>
          </div>
        </div>
        <div>
          <div class="ball">
            <div class="inner inner-hook"></div>
          </div>
        </div>
        <div>
          <div class="ball">
            <div class="inner inner-hook"></div>
          </div>
        </div>
        <div>
          <div class="ball">
            <div class="inner inner-hook"></div>
          </div>
        </div>
        <div>
          <div class="ball">
            <div class="inner inner-hook"></div>
          </div>
        </div>
      </div>
      <div class="shopcart-list">
        <div class="list-header">
          <h1 class="title">购物车</h1>
          <span class="empty">清空</span>
        </div>
        <div class="list-content" ref="list-content">
          <ul>
            <li class="food" v-for="(food,index) in selectFoods" :key="index">
              <span class="name">{{ food.name }}</span>
              <div class="price">
                <span>￥{{ food.price*food.count }}</span>
              </div>
              <!--<cartcontrol></cartcontrol>-->
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import cartcontrol from '../cartcontrol'	
  
export default {
  components:{
    cartcontrol
  },
  props:{
    seller:{
      type:Object
  },
  selectFoods:{
    type:Array,
    default(){
      return [];
    }
  }
  },
  data(){
    return {
    }
  },
  computed:{
    caculate(){
    if(this.calcuPrice === 0){  //如果初始价格为0
      return "￥"+this.seller.minPrice+"元起送";
    }else if(this.calcuPrice < this.seller.minPrice){
      return "还差"+(this.seller.minPrice - this.calcuPrice)+"元起送";
    }else{
      return "去结算";
    }
  },
  totalCount(){  //计算总数量
    let count=0;  
    this.selectFoods.forEach(food => {
      count += food.count;
    });
    return count;
  },
  calcuPrice(){   //计算总价格
    let pc = 0;  
    this.selectFoods.forEach(food => {
      pc += food.price*food.count;
    });
    return pc;
  }
  },
  methods:{
    toPay(){
      alert("该功能正在改造中...");
    }
  },
  name:'shopcart'
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang='stylus'>
@import '../../common/stylus/mixin.styl'

.shopcart 
  position: fixed
  left: 0
  bottom: 0
  height: 48px
  z-index: 50
  width: 100%
  .content 
    background: #141d27
    height: 48px
    display: flex
    font-size: 0
    .content-left 
      flex: 1
      .logo-wrapper 
        display: inline-block
        vertical-align: top
        position: relative
        margin: 0 12px
        padding: 6px
        width: 56px
        height: 56px
        box-sizing: border-box
        border-radius: 50%
        background: #141d27
        top: -10px
        .logo
          width: 100%
          height: 100%
          border-radius: 50%
          text-align: center
          color: #2b343c
          &.active
            background: #00a0dc
          .icon-shopping_cart
            line-height: 44px
            font-size: 24px
            color: #80858a
            &.active
              color: #fff
      .num 
        position: absolute
        line-height: 16px
        background: #f01414
        color: #fff
        font-size: 10px
        font-weight: 700
        width: 24px
        height: 16px
        top: 0
        right: 0
        text-align: center
        border-radius: 8px
      .price 
        display: inline-block
        vertical-align: top
        margin-top: 12px
        line-height: 24px
        padding-right: 12px
        box-sizing: border-box
        border-right: 1px solid rgba(255, 255, 255, 0.1)
        font-size: 16px
        font-weight: 700
        color: rgba(255, 255, 255, 0.4)
      .description 
        display: inline-block
        margin: 12px 0 0 12px
        font-size: 10px
        color: rgba(255,255,255,0.4)
        line-height: 24px
    .content-right 
      flex: 0 0 105px
      width: 105px
      .pay 
        line-height: 48px
        font-size: 12px
        font-weight: 700
        color: rgba(255,255,255,0.4)
        background: #2b333b
        text-align: center
        &.active 
          background: #00b43c
          color: #fff
</style>
