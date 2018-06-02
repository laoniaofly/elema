<template>
  <div class="cartcontrol">
    <transition name="move">
      <div class="decrease" v-show="food.count>0">
        <span class="inner icon-remove_circle_outline" @click.stop.prevent="delCart"></span>
      </div>
    </transition>
    <div class="count" v-show="food.count>0">{{ food.count }}</div>
    <div class="add icon-add_circle" @click.stop.prevent="addCart($event)"></div>
  </div>
</template>

<script>
export default {
  props:{
    food:{
      type:Object
    }
  },
  data () {
    return {
    }
  },
  methods:{
    delCart(){
      if(this.food.count){
          this.food.count--;
      }
    },
    addCart(event){
      if(!this.food.count){
        this.$set(this.food,'count',1);
      }else{
        this.food.count++;
      }
//		this.$store.commit({
//      type: 'initBallEle',
//      el: event.target
//    })
       this.$root.$emit('add_cart');
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang='stylus'>
  .cartcontrol 
    font-size: 0
    .decrease 
      display: inline-block
      padding: 6px
      transition: all 0.4s linear
      .inner
        display: inline-block
        color: #00a0dc
        line-height: 24px
        font-size: 24px
        transition: all 0.5s linear
      &.move-enter,&.move-leave-active
        opacity: 0
        transform: translate3d(24px,0,0)
        .inner
          transform: rotate(180deg)
    .count 
      display: inline-block
      vertical-align: top
      padding-top: 6px
      width: 12px
      line-height: 24px
      text-align: center
      font-size: 10px
      color: #93999f
    .add
      display: inline-block
      font-size: 24px
      line-height: 24px
      color: #00a0dc
      padding: 6px
</style>
