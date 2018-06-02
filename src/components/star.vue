<template>
  <div class="star" :class=" 'star_'+size ">
    <span class="star-item" :class=" score>=1?'on':'off' "></span>
    <span class="star-item" :class=" score>=2?'on':'off' "></span>
    <span class="star-item" :class=" score>=3?'on':'off' "></span>
    <span class="star-item" :class=" score>=4?'on':'off' "></span>
    <span class="star-item" :class=" score>=5?'on':'off' "></span>
  </div>
</template>

<script>
export default {
  props:{
    size:{
      type:Number
    },
    score:{
      type:Number
    }
  },
  name:'star'
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang='stylus'>
@import '../common/stylus/mixin.styl'
  .star 
    display: inline-block
    vertical-align: top
    font-size: 0
    .star-item 
      display: inline-block
      margin-right: 6px
      width: 15px
      height: 15px
      background-size: 15px 15px
      &:last-child 
        margin: 0
      &.on 
        bg-image('../common/image/star/star24_on')
      &.off 
        bg-image('../common/image/star/star24_off')
    &.star_24 
      margin: 0
      .star-item 
        margin-right: 3px
        width: 10px
        height: 10px
        background-size: 10px 10px
    &.star_48 
      .star-item 
        margin-right: 22px
        width: 20px
        height: 20px
        background-size: 20px 20px
</style>
