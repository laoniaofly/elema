<template>
	<div class="cartcontrol">
		<transition name="move">
			<div class="decrease" v-show="food.count>0">
				<span class="inner icon-remove_circle_outline" @click.stop.prevent="delCart">-</span>
			</div>
		</transition>
		<div class="count" v-show="food.count>0">{{ food.count }}</div>
		<div class="add icon-add_circle" @click.stop.prevent="addCart($event)">+</div>
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
<style scoped>
	.cartcontrol{
		font-size: 0;
	}
	.cartcontrol .decrease{
		display: inline-block;
		/* transition: all 0.4s linear; */
	}
	.cartcontrol .decrease .inner.move-enter{
		opacity: 0;
	}
	.cartcontrol .count{
		display: inline-block;
		vertical-align: top;
		width: 12px;
		line-height: 20px;
		text-align: center;
		font-size: 12px;
		color: #93999f;
	}
	.cartcontrol .add,
	.cartcontrol .decrease{
		display: inline-block;
		font-size: 20px;
		color: #fff;
		line-height: 14px;
		width: 16px;
		height: 16px;
		text-align: center;
		background: #00a0dc;
		border-radius: 50%;
		border: 2px solid #00a0dc;
		font-weight: 400;
		margin: 0 6px;
	}
	.cartcontrol .decrease{
		background: #fff;
		color: #00a0dc;
	}
</style>
